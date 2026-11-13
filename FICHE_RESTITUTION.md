# TP 1 — Publication d’un site statique dans Amazon S3

## Informations à compléter après votre configuration AWS

- **Prénom et nom :** À compléter
- **Région du projet (settings.aws.com) :** À compléter
- **Nom du bucket :** À compléter
- **URL publique du site (Bucket website endpoint) :** À compléter

## Questions

### 1. Quel service AWS avez-vous utilisé pour stocker et publier vos fichiers ?
Amazon S3 (Simple Storage Service), avec la fonction d’hébergement de site web statique.

### 2. Ce service relève-t-il de IaaS, PaaS ou SaaS ? Justifiez en deux phrases.
Dans ce TP, S3 est utilisé comme un service managé de stockage et d’hébergement, que l’on peut rapprocher du PaaS pour l’usage présenté. AWS gère l’infrastructure sous-jacente, tandis que l’utilisateur dépose ses fichiers et configure les accès ; il n’administre pas de serveur virtuel.

### 3. Qui gère le matériel physique et le centre de données ? Et vous, quelles responsabilités avez-vous ?
AWS gère les centres de données et le matériel physique. Je reste responsable de mes fichiers, de leur contenu, de la configuration des permissions et de la surveillance des dépenses.

### 4. Pourquoi votre site ne doit-il contenir aucune donnée sensible ?
Parce que les objets du site sont lisibles publiquement sur Internet. Une donnée personnelle, un secret ou une information médicale pourrait ainsi être consulté et diffusé par n’importe qui.

### 5. Que permet exactement l’autorisation `s3:GetObject` ?
Elle permet de lire ou télécharger les objets du bucket correspondant à la ressource indiquée dans la politique. Elle n’autorise ni le dépôt (`PutObject`) ni la suppression (`DeleteObject`).

### 6. Quelle action avez-vous menée pour surveiller les coûts ?
À compléter après la création : j’ai créé un budget AWS mensuel nommé `budget-b3com-nom-prenom`, fixé à **[montant] USD**, avec une notification envoyée à mon adresse e-mail.

## Liste de contrôle avant démonstration

- [ ] Le site s’ouvre dans une fenêtre privée.
- [ ] Le titre « Pharmacie Santé Plus » s’affiche.
- [ ] L’image est visible et la mise en forme verte est appliquée.
- [ ] Mon prénom et mon nom figurent sur la page.
- [ ] Le budget/alerte de coût existe.
- [ ] Le bucket ne contient aucune donnée personnelle, mot de passe ou clé.
- [ ] Capture 1 : budget et montant.
- [ ] Capture 2 : contenu du bucket (`index.html`, `style.css`, `images/pharmacie.jpg`).
- [ ] Capture 3 : site dans une fenêtre privée avec l’adresse visible.

> Cette fiche est un modèle : renseignez uniquement les informations effectivement constatées dans votre compte AWS. Les ressources AWS et les trois captures ne sont pas créées automatiquement par ce dépôt.
