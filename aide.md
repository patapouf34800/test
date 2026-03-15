# Mon Suivi Santé — Guide d'utilisation

## 🔐 Sécurité & données

Toutes vos données sont stockées **localement dans votre navigateur** (localStorage chiffré). Rien n'est envoyé sur un serveur.

### Mot de passe maître
Au premier lancement, vous devez choisir un mot de passe maître. Il chiffre toutes vos données avec AES-256. **Si vous perdez ce mot de passe, vos données locales sont irrécupérables** — pensez à exporter régulièrement.

### Export / Import
- **Exporter** : sauvegarde un fichier JSON lisible
- **🔒 Chiffré** : sauvegarde un fichier JSON chiffré (partageable avec mot de passe)
- **Importer** : restaure depuis un fichier JSON (chiffré ou non)

---

## 📊 Dashboard

Vue d'ensemble de vos données sur la période sélectionnée (mois en cours, mois précédent, tout).

Les KPIs affichés :
- **Déficit total** : calories objectif − calories consommées
- **Perte estimée** : déficit / 7700 kcal/kg
- **Poids théorique** : poids initial − perte estimée (basé sur les déficits depuis le début)
- **Dernière pesée** : votre dernier poids enregistré
- **Moy. calories** : moyenne journalière sur la période
- **Jours en déficit** : nombre de jours sous l'objectif calorique
- **Vélo (période)** : distance totale pédalée

---

## ⚖️ Poids

Suivi de votre évolution pondérale avec :

- **Courbe théorique** (orange) : progression calculée uniquement depuis les déficits caloriques
- **Courbe théorique+vélo** (bleu pointillé) : idem en ajoutant les calories brûlées à vélo depuis le 01/03
- **Modèle Hall** (violet) : projection réaliste avec adaptation métabolique (modèle NIH)
- **Fourchettes optimiste/pessimiste** : variation de ±6-10% selon l'adhérence
- **Pesées réelles** (points verts) : vos mesures réelles

### Enregistrer une pesée
Saisissez la date et le poids mesuré. L'écart vs théorique s'affiche automatiquement. Une icône ⚠️ apparaît si la pesée dépasse le seuil théorique même en comptant le vélo.

### Boutons de projection
- **Actuel** : affiche uniquement l'historique, sans projection
- **J+30 / J+90 / J+180** : projette l'évolution sur la durée choisie

---

## 🧮 Calculateur

Recherche dans la base Ciqual (1 356 aliments) + vos références personnelles. Tapez au moins 2 lettres.

Pour chaque aliment, saisissez le grammage et ajoutez-le à la liste du jour. Le total calorique et les macros sont calculés automatiquement.

### Enregistrer la journée
Une fois la liste complète, cliquez **Enregistrer** pour sauvegarder les calories du jour.

---

## 📉 Déficit

Graphique en barres de vos apports caloriques journaliers vs l'objectif. Filtrable par période.

---

## 🥗 Nutriments

Suivi des macronutriments (protéines, glucides, lipides, fibres) par jour. Nécessite d'utiliser le Calculateur avec des aliments ayant des données macro.

---

## 📅 Bilan hebdo

Récapitulatif semaine par semaine : calories moyennes, déficit, pesées de la semaine.

---

## 📚 Références

Vos aliments personnalisés avec calories/100g et macros optionnelles. Ils apparaissent en priorité dans le Calculateur.

Pour ajouter une référence : nom, calories/100g, puis optionnellement protéines, glucides, lipides, fibres.

---

## 🍲 Recettes

Créez des recettes combinant plusieurs aliments. La recette est automatiquement ajoutée à vos références avec les macros calculées.

---

## 🔬 Données macro

Explorateur de la base Ciqual avec filtres et tri par nutriment.

---

## 🚴 Vélo

Enregistrez vos sessions : date, distance (km), durée (min). Les calories brûlées sont estimées via la formule MET × poids × durée.

### Saisie vélo
Formulaire rapide d'ajout de session.

---

## ⚠️ À surveiller

Analyse automatique de votre dernier bilan sanguin. Les marqueurs hors norme sont affichés avec :
- **Rouge** : marqueurs vraiment anormaux
- **Vert** : marqueurs atypiques mais expliqués par une condition chronique déclarée

### Conditions chroniques
Cliquez sur "Conditions chroniques" (menu déroulant en bas) pour déclarer vos pathologies connues (bêta-thalassémie, hypothyroïdie, etc.). Les marqueurs concernés sont alors interprétés dans ce contexte.

---

## 🫀 Tension artérielle

Enregistrez vos mesures : date, systolique, diastolique, pouls.

Les zones OMS sont affichées :
- 🟢 **Optimale** : Sys < 120 et Dia < 80
- 🟡 **Normale** : Sys 120–129 et Dia ≤ 84
- 🟠 **Normale haute** : Sys 130–139 et Dia 85–89
- 🔴 **Hypertension G1** : Sys 140–159 ou Dia 90–99
- 🔴 **Hypertension G2** : Sys ≥ 160 ou Dia ≥ 100

Une **alerte automatique** s'affiche si la moyenne de vos 3 dernières mesures dépasse la zone "Normale".

---

## 🩸 Bilans sanguins

Importez vos bilans au format JSON. Chaque bilan est daté et contient vos marqueurs biologiques organisés par catégorie (hématologie, biochimie, lipides, vitamines, etc.).

Les valeurs sont colorées selon leur statut (normal / hors norme) et comparées bilan à bilan.

---

## 🔥 Besoin journalier (TDEE)

Calcul de votre dépense énergétique totale via la formule Mifflin-St Jeor × coefficient d'activité.

Renseignez sexe, âge, taille, poids et niveau d'activité. L'objectif calorique est recalculé automatiquement selon votre poids actuel.

---

## 🔗 Corrélations

Analyse la relation entre vos marqueurs sanguins et vos données quotidiennes (calories, déficit, poids). Utile pour identifier des tendances sur la durée.

---

## 📄 Rapports PDF

Deux types de rapports :

### Bilan personnel
Rapport sombre avec vos KPIs : poids, alimentation, vélo, marqueurs clés, nutrition.
Personnalisable par période (30/90/180 jours ou tout l'historique) et par section.

### Rapport médical
Rapport clair destiné à votre médecin avec :
- Vos conditions chroniques et leur impact sur la lecture des marqueurs
- Les marqueurs hors norme avec interprétation
- L'ensemble de vos bilans biologiques comparés bilan à bilan
- Vos 5 dernières mesures de tension avec alerte si nécessaire

---

## 💡 Conseils d'utilisation

- **Pesez-vous le matin à jeun** pour des mesures cohérentes
- **Enregistrez vos calories chaque jour** même approximativement — la tendance compte plus que la précision
- **Exportez régulièrement** vos données chiffrées comme sauvegarde
- Le poids théorique peut diverger de la réalité à cause de l'hydratation — c'est normal sur le court terme
- Si votre pesée est au-dessus du théorique+vélo, c'est un signal à investiger côté alimentation
