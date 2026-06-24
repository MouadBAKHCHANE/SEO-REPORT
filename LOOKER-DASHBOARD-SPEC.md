# DASHBOARD LOOKER STUDIO — NaoEnergy · Document de montage build-ready

Rapport mensuel · Audience : Charline (marketing, non technique) · 3 pages : Trafic & Devis · Google Ads · Agenda

---

## 1) RÉGLAGES GLOBAUX

### 1.1 Sources de données à connecter
| # | Connecteur | Cible exacte | Usage |
|---|-----------|--------------|-------|
| S1 | **Google Analytics (GA4)** | Propriété NaoEnergy, mesure **G-BG54VSLT7J** | Source principale page 1 & croisée page 2 |
| S2 | **Google Ads** | Compte **NAOenergy** | Source principale page 2 |
| S3 | **Search Console** | Site **naoenergy.ch** — 2 sources : **« Impression du site »** (Pays/Requêtes) + **« Impression de l'URL »** (pages) | Bas de page 1 |
| S4 | **Google Sheet** *(optionnel)* | Sheet « Plan d'action » (Action, Pourquoi, Échéance, Priorité, Statut) | Page 3 |

⚠️ Sur S2 : filtre de source **`Conversion action name = Lead site`** → évite de re-gonfler.

### 1.2 Période & comparaison
- 1 **Date range control** report-level (partagé). Défaut « Ce mois-ci ». **Comparaison = Période précédente** (flèches + %). Page 3 = aucun contrôle.

### 1.3 Charte
- turquoise #7CB1C4 · foncé #233036 · vert #2E7D5B (SEO) · bleu #2D6CB5 (Ads) · rouge #C0392B / orange #E08A1E (alertes). Police Roboto. Coins `border-radius:0 20px`.
- **Couleurs par canal verrouillées** : Ads=bleu, SEO=vert, Direct=gris, Social=turquoise.

### 1.4-1.7 En-tête (logo + titre + date) · Pied de page · Partage (Charline=Lecteur + diffusion PDF mensuelle) · Rafraîchissement 12h (GSC = 2-3 j de décalage).

---

## 2) PAGES

### PAGE 1 — 📈 Trafic & Demandes de devis
**Filtres** : exclure trafic interne (`Test data filter name ≠ internal` + secours `IP ≠ 196.75.123.176`) · drop-downs Canal / Pays.
**6 KPI (compar. M-1)** : Visiteurs · Visites · Nouveaux visiteurs · **Demandes de devis (accent)** · Taux de demande · Clics SEO (GSC).
**Graphes GA4** : 1) Time series Trafic+Leads · 2) Donut Nouveaux/connus · 3) Bar Canaux · 4) **Bar LEADS par canal (point fort)** · 5) Table Pages · 6) Geo map.
**Search Console (bas, encadré « décalage 2-3 j »)** : 7) Position moyenne (flèche inversée) · 8) Visibilité (impressions+clics) · 9) Top requêtes.

### PAGE 2 — 💰 Google Ads
**Filtres** : Conversions=Lead site · Enabled · drop-downs Campagne/Type/Réseau.
**8 KPI** : Budget (CHF) · **Demandes de devis** · **CPL (flèche inversée)** · Clics · CPC (inversée) · CTR · Taux conv. · Affichages.
**Graphes** : 1) Dépense+leads · 2) CPL dans le temps · 3) Donut budget par type · 4) Comparatif campagnes M-1 · 5) **Tableau perf par campagne (heatmap CPL feu tricolore)** · 6) **Alerte budget sans demande (rouge)** · 7) Mots-clés TOP · 8) Mots-clés FLOP (gaspillage).

### PAGE 3 — 🗓️ Agenda (statique)
6 cartes-jalons (verrou ~34, démotion BS-10% ~5 juil, Odoo→offline, Search-Générique, doublons, avancement) · mini-timeline S1-S4 · **Tableau Plan d'action** (Action | Pourquoi | Échéance | Priorité | Statut) · légende.

---

## 3) RENOMMAGES FR (clé)
Active users→**Visiteurs** · Sessions→**Visites** · New users→**Nouveaux visiteurs** · generate_lead→**Demandes de devis** · Average Position→**Position moyenne** · Cost→**Budget (CHF)** · Avg CPC→**Prix moyen d'un clic** · CPL = Cost÷Conversions(Lead site).
Canaux : Organic Search→**Google naturel (SEO)** · Paid Search→**Google Ads** · Direct→**Accès direct** · Referral→**Sites référents**.

## 4) VIGILANCE
- **CPL = Cost ÷ Conversions « Lead site » uniquement** (jamais All conversions). Même déf. lead partout (GA4 generate_lead ↔ Ads Lead site, ~34 vrais/mois).
- Exclusion trafic interne (ceinture+bretelles). GSC = 2-3 j de décalage. Flèches inversées : Position, CPL, CPC. Page Agenda = 100% statique.
