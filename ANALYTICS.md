# Ajouter Plausible Analytics (recommandé) ou Google Analytics

## Option 1 : Plausible (recommandé)

**Avantages :**
- RGPD-compliant par défaut (pas besoin de bannière cookies)
- Léger (~1KB vs ~45KB pour GA)
- Interface claire, données essentielles
- Hébergé en Europe (Allemagne)
- 9€/mois jusqu'à 10k vues/mois

**Installation :**

1. Créer un compte sur https://plausible.io
2. Ajouter le domaine `major-exchanges.com`
3. Ajouter la ligne suivante dans le `<head>` de CHAQUE page HTML (juste avant `</head>`) :

```html
<script defer data-domain="major-exchanges.com" src="https://plausible.io/js/script.js"></script>
```

4. Vérifier la remontée des événements dans le dashboard Plausible après quelques heures.

**Astuce :** tu peux créer un fichier `assets/analytics.html` avec juste cette ligne et l'inclure via JS, mais vu que tu n'as que 12 pages, la copie manuelle est plus simple.

---

## Option 2 : Google Analytics 4 (gratuit mais RGPD contraignant)

**Installation :**

1. Créer une propriété GA4 sur https://analytics.google.com
2. Récupérer ton ID de mesure (format `G-XXXXXXXXXX`)
3. Ajouter dans le `<head>` de chaque page :

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX', {
    anonymize_ip: true,
    cookie_flags: 'SameSite=None;Secure'
  });
</script>
```

4. ATTENTION RGPD : avec Google Analytics, tu DOIS afficher une bannière cookies avec consentement explicite (sinon amende CNIL). Utilise **tarteaucitron.io** ou **cookiebot** pour gérer ça.

---

## Option 3 : Analytics auto-hébergé sur ton VPS Hostinger

Vu que tu as déjà un VPS Hostinger avec Node.js pour tes autres projets, tu peux héberger **Umami** (open-source, RGPD-compliant, gratuit) :

```bash
# Sur ton VPS
git clone https://github.com/umami-software/umami.git
cd umami
npm install
# Configurer la base de données (PostgreSQL ou MySQL)
npm run build
npm start
```

Puis même snippet que Plausible mais avec ton domaine :
```html
<script defer src="https://analytics.tondomaine.com/script.js" data-website-id="TON_ID"></script>
```

**Avantages :** gratuit, full ownership des données, RGPD OK sans bannière si configuré correctement.

---

## Conseil

Pour un site pro comme Major Exchanges qui cible des clients institutionnels (DRH, cabinets), je recommande **Plausible** :
- Le message "zero cookies, zero tracking" rassure tes prospects
- Pas de bannière de consentement à gérer
- Métriques claires (visiteurs, sources, pages populaires, conversions)
- Coût très modéré (9€/mois)

Les 9€/mois se rentabilisent dès le premier lead B2B qualifié.
