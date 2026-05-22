# Incident 2026-05-22 — 5 pages blanches LIVE

## TL;DR
**Cause :** Service YouTube de Complianz buggué → PHP fatal silencieux sur les pages contenant un bloc YouTube embed.
**Fix appliqué :** Désactivation du service YouTube dans Complianz → Intégrations → Services.
**Statut :** ✅ Les 5 pages rechargent normalement.

## Pages impactées (HTTP 200, body vide)
- /solutions/pompes-a-chaleur/ (post 121)
- /solutions/batteries-de-stockage/ (post 129)
- /qui-sommes-nous/ (post 307)
- /regroupement-de-proprietaire-suisse/ (post 452)
- /la-charte-commerciale-responsable/ (post 10075)

## Diagnostic (chronologie)
1. Test bulk 18 URL → 5 cassées, 13 OK.
2. REST API renvoie le contenu intact → BDD OK, fatal côté thème/plugin.
3. Headers HTTP des pages cassées : `Set-Cookie: PHPSESSID`, `expires: 1981`, `pragma: no-cache` → WP Rocket refuse de cacher car erreur serveur.
4. Croisement classes CSS via REST → **100% des pages cassées contiennent `wp-block-embed-youtube`** ; 0% des pages OK.
5. Test #1 : forcer re-fetch oEmbed via Gutenberg sur `/qui-sommes-nous/` → ❌ pas de changement (pas un problème de cache oEmbed obsolète).
6. Test #2 : désactiver "WP Rocket Lazyload iframes" → ❌ pas de changement (option restaurée).
7. Test #3 : désactiver "Complianz → Services → YouTube" → ✅ **les 5 pages reviennent en ~300 KB**.

## Action à prévoir (RGPD)
Désactiver le service YouTube de Complianz **enlève le consentement cookies tiers pour YouTube**. Risque RGPD/LPD léger. Options :

1. **Mettre à jour Complianz** → si version pas à jour, le bug est probablement corrigé.
2. **Workaround custom** : remplacer les blocs YouTube par des `<iframe youtube-nocookie>` ou un placeholder maison qui charge la vidéo après clic utilisateur (consentement implicite).
3. **Statu quo court terme** : YouTube embeds appellent youtube.com sans cookie consent géré → acceptable 1-2 semaines le temps de fixer.

## Validation
- 5 pages cassées : HTTP 200, contenu présent (220-310 KB).
- Pages saines : pas de régression (homepage, /notre-equipe/, /solutions/panneaux-photovoltaiques/, etc.).
