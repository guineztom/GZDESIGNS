# GZ Designs — Site web

## Déploiement sur Cloudflare Pages (drag & drop, sans GitHub)

### Option A — Sans GitHub (le plus simple)

1. Va sur **cloudflare.com** → crée un compte gratuit
2. Dans le menu : **Pages** → **Create a project** → **Direct Upload**
3. Donne un nom au projet (ex: `gz-designs`)
4. **Compresse ce dossier en .zip** et glisse-le dans la zone d'upload
5. Cloudflare te donne une URL en `.pages.dev` — ton site est en ligne !
6. Pour connecter ton domaine : **Pages** → ton projet → **Custom domains**

### Option B — Avec GitHub (pour le CMS Decap)

Pour que le CMS `/admin` fonctionne, il faut GitHub :

1. Crée un repo GitHub (peut être privé) et pousse ce dossier
2. Sur Cloudflare Pages → **Connect to Git** → sélectionne ton repo
3. Build settings : pas de build command, output directory = `/`
4. Dans ton repo GitHub → **Settings** → **Pages** → active GitHub Actions
5. Active **Cloudflare Pages** pour les deployments automatiques

### Activer le CMS (/admin)

Le CMS nécessite Netlify Identity ou Cloudflare Access pour l'authentification.

**Solution la plus simple : Git Gateway via Netlify**
(même si le site est sur Cloudflare, tu peux utiliser Netlify Identity juste pour l'auth)

1. Crée un compte sur app.netlify.com
2. **Identity** → Enable Identity → **Git Gateway** → Enable Git Gateway
3. Invite ton email dans Identity → Accepte l'invitation
4. Accède à `ton-site.pages.dev/admin` → connecte-toi

**Alternative encore plus simple : éditer les fichiers JSON directement**
Les fichiers dans `/content/*.json` contiennent tout le texte éditable.
Tu peux les modifier directement sur GitHub (interface web) sans passer par le CMS.

### Configurer Formspree (formulaire de contact)

1. Va sur **formspree.io** → crée un compte gratuit
2. **New Form** → donne-lui un nom → copie l'ID (ex: `xbjnkpqr`)
3. Dans `index.html`, cherche `VOTRE_ID_FORMSPREE` et remplace par ton ID
4. Dans `content/contact.json`, mets ton ID dans `formspree_id`

### Mettre à jour le site

**Sans CMS** : modifie les fichiers HTML/JSON → re-zip → re-upload sur Cloudflare Pages
**Avec CMS** : va sur `ton-domaine.fr/admin` → modifie → Save → le site se met à jour auto

### Structure des fichiers

```
gz-designs/
├── index.html          ← Page principale
├── cgv.html            ← Conditions Générales de Vente
├── sitemap.xml         ← Pour Google
├── robots.txt          ← Pour Google
├── _redirects          ← Cloudflare Pages routing
├── _headers            ← Headers sécurité
├── admin/
│   ├── index.html      ← Interface CMS
│   └── config.yml      ← Configuration CMS (champs éditables)
└── content/
    ├── hero.json       ← Textes hero
    ├── process.json    ← Les 4 étapes
    ├── why.json        ← Section pourquoi
    ├── pricing.json    ← Tarifs
    ├── faq.json        ← FAQ
    ├── contact.json    ← Section contact
    └── meta.json       ← SEO
```

### Personnalisation rapide

- **Ton email dans Formspree** : c'est configuré dans ton dashboard Formspree
- **Ton domaine** : à connecter dans Cloudflare Pages → Custom domains
- **Les images du carrousel** : remplace les URLs Unsplash dans `index.html` par tes propres photos
- **Les tarifs** : modifiables dans `content/pricing.json` ou directement dans `index.html`
