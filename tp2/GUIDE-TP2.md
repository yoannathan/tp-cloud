# TP2 — Protéger et restaurer le site de la pharmacie

Ce dossier prépare les fichiers locaux du TP2. **Il ne modifie pas AWS.** Les changements de versioning, téléversements, suppressions simulées, création du bucket privé, téléchargements, tests d’accès et captures doivent être réalisés dans votre console, dans les deux buckets qui vous appartiennent. N’envoyez jamais de secrets dans GitHub.

## Arborescence de travail

- `reference/` : copie de référence intacte des fichiers du site.
- `travail/` : version 2 prête à tester et publier.
- `incident/index.html` : page erronée à téléverser uniquement pour simuler l’incident 1.
- `recuperation/` : destination des versions restaurées depuis AWS.
- `sauvegarde-v2/` : copie locale de secours à valider avant archivage.
- `pharmacie-v2.zip` : archive de cette copie, destinée uniquement au second bucket privé.

Les sous-dossiers reference/travail/recuperation/sauvegarde-v2 doivent contenir les fichiers du site (`index.html`, `style.css`, `images/pharmacie.jpg`). Ne modifiez jamais la référence. Les répertoires de récupération et de sauvegarde sont des emplacements personnels locaux ; leur contenu n’est pas synchronisé vers AWS par ce guide.

## Ordre du TP et précautions

1. Vérifiez d’abord que le site du TP1 fonctionne et notez son endpoint HTTP, sa région et son bucket. Réparez le TP1 avant de simuler un incident.
2. Copiez les fichiers du TP1 dans `reference/`, puis dupliquez-les dans `travail/`. La version 2 préparée ici conserve les styles et l’image et modifie les horaires en **8 h à 21 h (horaires fictifs)**, avec la mention `Version 2 - TP2 - Site de démonstration.` Testez-la localement avant toute publication.
3. Activez le versioning sur le bucket du site. Vérifiez qu’il est `Enabled` et prenez P1. Le versioning n’invente pas les versions antérieures à son activation.
4. Téléversez uniquement `travail/index.html` à la racine du bucket du site. Vérifiez le site en fenêtre privée, puis identifiez dans l’historique l’ID AWS exact de la version 2. Prenez P2 et P3 ; ne continuez pas si l’historique ou l’identifiant n’est pas visible.
5. Pour l’incident 1, téléversez `incident/index.html` à la racine du bucket du site. Pour restaurer, téléchargez depuis l’historique **la version identifiée de la version 2**, placez-la dans `recuperation/`, vérifiez le contenu, puis téléversez ce fichier restauré à la racine. Cela crée une nouvelle version actuelle ; ne supprimez aucune ancienne version.
6. Pour l’incident 2, effectuez uniquement une suppression simple de `index.html` (pas une suppression par version ID). Activez `Show versions`, identifiez le marqueur de suppression le plus récent de `index.html`, et demandez à l’enseignant de vérifier la sélection. Supprimez **ce marqueur seulement**. Ne cochez aucune version de fichier. Cette opération rend la dernière version conservée actuelle sans nouveau téléversement.
7. Préparez `sauvegarde-v2/` avec le `index.html` V2 vérifié et les fichiers CSS/image du TP1. Ouvrez le site local depuis le dossier et vérifiez image, style, horaires et mention V2. Compressez le dossier en `pharmacie-v2.zip`.
8. Créez un deuxième bucket dans la même région. Gardez **Block all public access** activé, ACL désactivées, hébergement de site statique désactivé et aucune politique publique. Téléversez uniquement `pharmacie-v2.zip` dans ce bucket privé. Ne placez jamais l’archive dans le bucket public du site.
9. Copiez l’Object URL directe de l’archive et testez-la dans une fenêtre privée sans session. Un refus 403/AccessDenied est attendu ; ne créez pas d’URL présignée pour ce test. Ensuite, téléchargez l’archive depuis la console avec votre session, extrayez-la dans `test-restauration/` et vérifiez le site.
10. Relisez la politique du bucket public du site, vérifiez qu’elle accorde uniquement `s3:GetObject` sur les objets de ce bucket et qu’aucune archive ou donnée confidentielle n’y est présente. Consultez le budget du TP1 sans changer son seuil ; notez le montant affiché et l’heure. Masquez l’adresse e-mail sur P10 avant remise.
11. Complétez `fiche-tp2.txt` avec les identifiants et heures observés. Joignez P1 à P10. Conservez les deux buckets jusqu’à validation de l’enseignant.

## Règles de sécurité essentielles

- Ne jamais supprimer définitivement une version de fichier pendant les incidents.
- Ne jamais supprimer un marqueur avant d’avoir identifié et fait vérifier le marqueur exact créé lors de votre exercice.
- Ne rendre jamais le bucket de secours public.
- Ne jamais y activer l’hébergement statique ; ne jamais y déposer le ZIP dans le bucket du site public.
- Le versioning et deux buckets dans un seul compte ne protègent pas contre tous les scénarios de perte du compte. Le budget est une alerte, pas un plafond.
- Aucune donnée personnelle ou médicale réelle, clé d’accès, mot de passe ou code de sécurité dans le contenu, les captures ou le dépôt Git.

## Captures exigées

- **P1** versioning activé ; **P2** site V2 en fonctionnement ; **P3** historique et identifiant AWS de V2 ; **P4** site restauré après l’incident 1 ; **P5** marqueur et versions conservées ; **P6** site après retrait du marqueur ; **P7** bucket de secours privé ; **P8** refus anonyme de l’URL directe ; **P9** archive téléchargée, extraite et fonctionnelle ; **P10** budget consulté avec adresse e-mail masquée.

Les captures sont à produire vous-même dans AWS ; aucune valeur ou opération AWS n’est simulée par les fichiers de ce dépôt.
