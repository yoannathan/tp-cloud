# TP 1 — Pharmacie Santé Plus

Mini-site statique de démonstration pour le module **Cloud Computing (B3COM0204)**. Il présente une pharmacie fictive de Douala et est organisé pour suivre le TP d’hébergement sur Amazon S3.

## Contenu

```text
.
├── index.html
├── style.css
├── images/
│   └── pharmacie.jpg
├── FICHE_RESTITUTION.md
└── README.md
```

Le site est autonome (HTML, CSS et image locale). Pour reproduire exactement l’arborescence du bucket demandée, téléversez uniquement `index.html`, `style.css` et le dossier `images/` à la racine du bucket. Le README et la fiche ne sont pas nécessaires au site.

## Personnalisation avant remise

1. Dans `index.html`, remplacez « À compléter : prénom et nom » par votre identité.
2. Remplacez le numéro fictif `+237 6 XX XX XX XX` par un contact que vous êtes autorisé à publier, ou gardez un numéro fictif clairement signalé.
3. Ouvrez `FICHE_RESTITUTION.md` et renseignez votre région, le nom réel du bucket et l’URL fournie par AWS.

## Publication sur Amazon S3 (console AWS)

Ce dépôt contient les fichiers et le guide, mais **ne crée pas de ressources AWS**. Le bucket, le budget et la politique publique doivent être configurés dans votre propre compte et dans la région attribuée à votre projet. N’ajoutez jamais de mot de passe ou de clé d’accès au dépôt.

1. Dans AWS, ouvrez **Billing and Cost Management → Budgets** et créez l’alerte mensuelle du TP (par exemple 1 USD), avec votre adresse e-mail.
2. Dans **Amazon S3**, créez un bucket unique de la forme `b3com-nom-prenom-XXXX`, dans la région de votre projet. Gardez le blocage public activé pendant le téléversement.
3. Envoyez `index.html` et `style.css` à la racine, puis `pharmacie.jpg` dans le dossier `images/`.
4. Dans **Properties → Static website hosting**, activez **Host a static website** et indiquez `index.html` comme document d’index.
5. Dans **Permissions**, désactivez le blocage d’accès public pour ce bucket seulement, puis appliquez la politique ci-dessous après avoir remplacé le nom du bucket.
6. Copiez le **Bucket website endpoint** et testez-le dans une fenêtre privée. S3 Website Endpoint est généralement servi en HTTP ; ne placez aucune donnée sensible sur le site.

Politique de lecture des objets du seul bucket :

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadForWebsite",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::b3com-nom-prenom-XXXX/*"
    }
  ]
}
```

Cette politique autorise la lecture (`s3:GetObject`) des objets ; elle ne donne pas au public le droit d’envoyer ou de supprimer des fichiers. Le budget signale un dépassement mais ne bloque pas automatiquement les coûts. N’activez aucun autre service pour ce TP et gardez le bucket jusqu’à sa validation par l’enseignant.

## Vérification locale

Ouvrez `index.html` dans un navigateur. La page est responsive. L’image est une illustration originale, pas la photo d’une personne.
