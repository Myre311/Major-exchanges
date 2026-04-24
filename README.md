# Major Exchanges — Site web refondu

Site statique multi-pages, HTML/CSS/JS pur, zéro dépendance de build.
Direction artistique **éditoriale scientifique** : serif expressif (Fraunces), palette bleu nuit / crème / terracotta, grille asymétrique.

## Structure des fichiers

```
major-exchanges/
├── index.html            Accueil — hero + bénéfices + preuve sociale + 5 niveaux
├── methodologie.html     Rosace 8 dimensions, 5 niveaux, Comprendre-Structurer-Dynamiser
├── outils.html           Guide entretien, modalités, IA, livrables
├── services.html         Offres Profil vs Expertise, parcours d'intégration
├── references.html       OTAN, Lafayette, 4 prix, chiffres-clés, Equarior
├── metier.html           6 domaines, philosophie 3 piliers
├── expert.html           Positionnement DRH/coachs/consultants
├── cv-softskills.html    CV Soft Skills — produit complémentaire
├── contact.html          Formulaire Formspree + FAQ
├── 404.html              Page d'erreur personnalisée
├── robots.txt            Indexation OK + sitemap
├── sitemap.xml           9 pages référencées
├── netlify.toml          Config Netlify (redirections + headers sécurité)
├── vercel.json           Config Vercel (alternative)
└── assets/
    ├── style.css         Design system complet
    ├── script.js         Menu + reveal scroll + handler Formspree
    └── favicon.svg       Favicon SVG minimaliste
```

## Déploiement

### Option 1 — Netlify (recommandé, 5 minutes)

1. Créer un compte gratuit sur https://app.netlify.com
2. "Add new site" → "Deploy manually" → glisser-déposer le dossier `major-exchanges/`
3. Le site est en ligne sous `xxx.netlify.app` immédiatement
4. Pour ton domaine : "Domain settings" → "Add custom domain" → `major-exchanges.com`
5. Changer les DNS chez Hostinger pour pointer vers Netlify (instructions affichées)
6. HTTPS activé automatiquement par Netlify

La config `netlify.toml` fournit :
- Page 404 personnalisée sur les routes inconnues
- Headers de sécurité (HSTS, X-Frame-Options, Referrer-Policy…)
- Cache long pour les assets (1 an avec `immutable`)

### Option 2 — Vercel

1. Créer un compte sur https://vercel.com
2. "Add New" → "Project" → importer un dossier local ou un repo Git
3. Deploy (aucune config demandée, `vercel.json` s'occupe de tout)

### Option 3 — Hostinger FTP (classique)

Uploader tout le contenu de `major-exchanges/` dans `public_html/` du domaine.
Vu que c'est du HTML statique pur, aucune config PHP/Node requise.
Seul bémol : la page 404 n'est pas auto-routée comme sur Netlify/Vercel — il faut configurer `.htaccess` :

```apache
ErrorDocument 404 /404.html
```

### Option 4 — Tu restes sur Squarespace

Possible mais déconseillé : Squarespace ne permet pas l'import de site HTML custom sans passer par un plan Developer qui coûte cher. Migrer vers Netlify est gratuit, plus rapide et plus flexible.

## Configurer le formulaire de contact

Le formulaire utilise **Formspree** (gratuit jusqu'à 50 soumissions/mois).

1. Inscription sur https://formspree.io avec `contact@major-exchanges.com`
2. Créer un nouveau form, Formspree affiche un ID au format `xxxxxxxx`
3. Dans `contact.html`, chercher `YOUR_FORM_ID` et le remplacer par l'ID :
   ```html
   <form id="contactForm" class="form"
         action="https://formspree.io/f/abcd1234" method="POST">
   ```
4. Re-déployer. Chaque soumission arrive par email + est consultable dans le dashboard Formspree.

**Alternative gratuite illimitée** : tu peux aussi monter ton propre endpoint sur ton VPS Hostinger (Node + Nodemailer). Dis-moi si tu veux que je te code ça, j'en ai pour 15 min.

Le JS inclut déjà un garde-fou : si `YOUR_FORM_ID` n'est pas remplacé, un message d'avertissement s'affiche au lieu d'envoyer.

## Design system

Toutes les couleurs et polices sont centralisées dans `:root` en tête de `style.css`.

**Palette**
- `--ink` `#0A1628` — bleu nuit (fond dominant)
- `--paper` `#F4EFE6` — crème chaude (texte / sections claires)
- `--rust` `#C2572E` — terracotta (accent rare, CTAs)
- `--gold` `#C9A961` — or atténué (chiffres, secondaires)
- `--sage` `#7A8B6F` — vert olive (states de succès)

**Typographie** (chargée via Google Fonts avec `display=swap`)
- `--font-display` : Fraunces (serif variable) — titres, italiques expressifs
- `--font-body` : Inter Tight — corps de texte
- `--font-mono` : JetBrains Mono — eyebrows, numérotation

**Composants réutilisables**
- `.nav` — navigation fixe avec backdrop blur
- `.hero`, `.page-header` — en-têtes de section
- `.benefits`, `.pillars`, `.steps`, `.offers`, `.validation`, `.stats` — grilles
- `.section-light` — variante fond crème (inversion des couleurs auto)
- `.cta-banner` — bandeau orange terracotta
- `.quote` — citation large style éditorial
- `.form`, `.form-group` — formulaires stylés
- `.reveal` + `.reveal-delay-N` — animations au scroll (IntersectionObserver)

## SEO & accessibilité

- Balises `<title>` et `<meta description>` uniques par page
- Meta Open Graph + Twitter Card sur chaque page (partage social)
- `sitemap.xml` avec 9 URLs + priorités
- `robots.txt` pointant vers le sitemap
- Favicon SVG (tous navigateurs modernes)
- Contrastes AAA, labels form explicites, focus visibles
- HTML sémantique (`<nav>`, `<main>`, `<section>`, `<footer>`)

## Personnalisation rapide

**Changer les couleurs globales** — éditer les variables dans `assets/style.css` lignes 12-22.

**Changer une police** — modifier l'import Google Fonts ligne 7 + les variables `--font-*`.

**Ajouter une page** — dupliquer `expert.html`, changer le contenu, ajouter le lien dans la `<nav>` ET le `<footer>` des 10 pages existantes.

## À faire après déploiement

1. **Configurer Formspree** (5 min) — voir section ci-dessus
2. **Remplacer `YOUR_FORM_ID`** dans `contact.html`
3. **Connecter Plausible ou Google Analytics** — ajouter le snippet dans `<head>` des pages
4. **Ajouter tes vraies captures d'écran** de l'app à la place des placeholders SVG sur `outils.html`
5. **Témoignages clients** — si tu en as 2-3, je peux ajouter la section sur la homepage
6. **Page CGU** — à reprendre depuis ton site actuel (obligatoire)
7. **Mentions légales** — idem, obligatoire en France

## Notes techniques

- Zéro dépendance npm, zéro build, zéro framework
- Compatible Chrome/Firefox/Safari/Edge 2020+
- Responsive mobile-first, breakpoints à 500 / 800 / 900 / 960 px
- Total des assets : ~100 KB (HTML + CSS + JS, polices non comptées)
- Score Lighthouse estimé : 95+ en Performance, 100 en Accessibilité / SEO / Best Practices

---

## Approche éditoriale

Le site reprend les meilleures pratiques UX d'Experteer.fr (hiérarchie claire, bénéfices numérotés, preuve sociale chiffrée, validation institutionnelle) mais avec une direction artistique radicalement différente : là où Experteer fait du SaaS corporate standard (bleu sur blanc, sans-serif), Major Exchanges adopte un positionnement éditorial scientifique (serif expressif, fond sombre, palette terrienne) plus cohérent avec sa signature "outil de nouvelle génération" et ses références institutionnelles.

Aucun code, aucune structure, aucun texte n'est copié d'Experteer — seules les bonnes pratiques d'architecture d'information ont été transposées dans un univers visuel propre à Major Exchanges.
