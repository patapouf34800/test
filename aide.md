# Mon Suivi Santé — Guide d'utilisation

## 🔐 Sécurité & données

Toutes vos données sont stockées **localement dans votre navigateur** (localStorage chiffré). Rien n'est envoyé sur un serveur.

### Mot de passe maître
Au premier lancement, vous choisissez un mot de passe maître qui chiffre toutes vos données avec AES-256 (PBKDF2 + AES-GCM). **Si vous perdez ce mot de passe, vos données locales sont irrécupérables** — exportez régulièrement.

### Export / Import
- **Exporter** : sauvegarde un fichier JSON lisible
- **🔒 Chiffré** : sauvegarde un fichier JSON chiffré par mot de passe — partageable en toute sécurité
- **Importer** : restaure depuis un fichier JSON (chiffré ou non). Si chiffré, le mot de passe est demandé

---

## 📊 Dashboard

Vue d'ensemble sur la période choisie (mois en cours, mois précédent, tout).

- **Déficit total** : calories objectif − calories consommées
- **Perte estimée** : déficit / 7700 kcal/kg
- **Poids théorique** : poids initial − perte calorique cumulée depuis le début
- **Dernière pesée** : dernier poids enregistré
- **Moy. calories** : moyenne journalière sur la période
- **Jours en déficit** : jours sous l'objectif calorique
- **Sport (période)** : distance totale sur les activités avec distance

---

## ⚖️ Poids

- **Courbe orange** : poids théorique basé sur les déficits caloriques depuis le début
- **Courbe bleue pointillée** : poids théorique étendu incluant les calories brûlées en sport depuis le 01/03
- **Modèle Hall** (violet) : projection réaliste avec adaptation métabolique (modèle NIH)
- **Fourchettes** optimiste/pessimiste : variation ±6–10% selon l'adhérence
- **Points verts** : pesées réelles

### Enregistrer une pesée
Date + poids. L'écart vs théorique s'affiche. Un ⚠️ rouge apparaît si la pesée dépasse le seuil théorique+sport.

### Projections
- **Actuel** : historique uniquement, sans projection
- **J+30 / J+90 / J+180** : projection sur la durée choisie

---

## 🧮 Calculateur

Recherche dans 1 356 aliments Ciqual + vos références personnelles. Tapez au moins 2 lettres, saisissez le grammage, ajoutez à la liste. Le total calorique et les macros sont calculés automatiquement.

Cliquez **Enregistrer** pour sauvegarder la journée.

---

## 📉 Déficit

Graphique en barres des apports caloriques journaliers vs l'objectif, filtrable par période.

---

## 🥗 Nutriments

Suivi des macronutriments (protéines, glucides, lipides, fibres) par jour. Nécessite d'utiliser le Calculateur avec des aliments ayant des données macro.

---

## 📅 Bilan hebdo

Récapitulatif semaine par semaine : calories moyennes, déficit, pesées.

---

## 📚 Références

Vos aliments personnalisés avec calories/100g et macros optionnelles. Apparaissent en priorité dans le Calculateur.

---

## 🍲 Recettes

Créez des recettes combinant plusieurs ingrédients. Les macros sont calculées automatiquement et la recette est ajoutée à vos références.

---

## 🔬 Données macro

Explorateur de la base Ciqual avec filtres et tri par nutriment.

---

## 🏃 Sport

Enregistrez vos sessions sportives : date, type d'activité, distance (si applicable), durée.

### Types d'activités disponibles
| Activité | MET | Distance |
|---|---|---|
| 🚴 Vélo intérieur | 4 | ✓ |
| 🚵 Vélo extérieur | 8 | ✓ |
| 🏃 Course à pied | 8 | ✓ |
| 🚶 Marche rapide | 4.5 | ✓ |
| 🏊 Natation | 7 | — |
| 🏋️ Musculation | 5 | — |
| ⚡ Autre | libre | — |

Les calories sont estimées via **MET × poids du jour × durée (h)**.

Le panneau Sport affiche **un bloc de graphiques par type d'activité** présent dans vos données : distance/durée, vitesse moyenne (si applicable), dépense calorique.

---

## ⚠️ À surveiller

Analyse automatique du dernier bilan sanguin importé. Deux catégories :
- **Rouge** : marqueurs vraiment hors norme
- **Vert** : marqueurs atypiques mais expliqués par une condition chronique déclarée

### Conditions chroniques
Menu déroulant en bas du panneau. Déclarez vos pathologies connues (bêta-thalassémie, hypothyroïdie, diabète...) pour que les marqueurs concernés soient interprétés dans ce contexte dans les bilans et rapports PDF.

---

## 🫀 Tension artérielle

Enregistrez vos mesures (systolique, diastolique, pouls). Zones OMS affichées :

- 🟢 **Optimale** : Sys < 120 et Dia < 80
- 🟡 **Normale** : Sys 120–129 et Dia ≤ 84
- 🟠 **Normale haute** : Sys 130–139 et Dia 85–89
- 🔴 **Hypertension G1** : Sys 140–159 ou Dia 90–99
- 🔴 **Hypertension G2** : Sys ≥ 160 ou Dia ≥ 100

Une **alerte automatique** s'affiche si la moyenne des 3 dernières mesures dépasse "Normale".

---

## 🩸 Bilans sanguins

Importez vos bilans au format JSON. Les valeurs sont colorées selon leur statut et comparées bilan à bilan par catégorie (hématologie, biochimie, lipides, vitamines, hormones).

---

## 🔥 Besoin journalier (TDEE)

Calcul de votre dépense énergétique via la formule Mifflin-St Jeor × coefficient d'activité. L'objectif calorique est recalculé automatiquement selon votre poids actuel.

---

## 🔗 Corrélations

Analyse la relation entre vos marqueurs sanguins et vos données quotidiennes (calories, déficit, poids).

---

## 📄 Rapports PDF

### Bilan personnel (style sombre)
KPIs poids, alimentation (déficit + déficit étendu avec sport), sport (distance, sorties, vitesse, calories), marqueurs sanguins clés, nutrition avec barres de progression vs cibles.

### Rapport médical (style clair)
Destiné à votre médecin :
- Conditions chroniques avec description et marqueurs impactés
- Marqueurs hors norme avec interprétation clinique
- Marqueurs atypiques contextualisés par condition
- Tous vos bilans biologiques comparés
- 5 dernières mesures de tension avec alerte si nécessaire

---

## 💡 Conseils

- Pesez-vous **le matin à jeun** pour des mesures cohérentes
- Enregistrez vos calories chaque jour, même approximativement — la tendance compte plus que la précision
- **Exportez régulièrement** vos données (export chiffré recommandé comme sauvegarde)
- Le poids théorique peut diverger de la réalité à cause de l'hydratation — c'est normal à court terme
- Si votre pesée dépasse le théorique+sport ⚠️, investiguez côté alimentation
