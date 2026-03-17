# Mon Suivi Santé — Guide d'utilisation

## 🚀 Premiers pas — Configuration initiale

Avant toute chose, rendez-vous dans **🔥 Besoin journalier** (sidebar) et renseignez vos paramètres personnels :

- **Sexe, âge, taille** — nécessaires pour le calcul du métabolisme de base (formule Mifflin-St Jeor)
- **Poids de départ** — point d'ancrage de toute la courbe théorique
- **Niveau d'activité** — coefficient multiplicateur du TDEE
- **Objectif calorique** — calculé automatiquement depuis votre TDEE, ajustable

Ces valeurs sont la base de **tous les calculs de l'application** : poids théorique, déficit, projections. Sans elles, les chiffres affichés n'ont pas de sens.

> 💡 Le poids de départ se renseigne dans le champ **Poids (kg)** en bas du panneau Besoin journalier. L'objectif calorique se recalcule automatiquement à chaque nouvelle pesée enregistrée.

---

## 🔐 Sécurité & données

Toutes vos données sont stockées **localement dans votre navigateur** (localStorage chiffré). Rien n'est envoyé sur un serveur.

### Mot de passe maître
Au premier lancement, vous choisissez un mot de passe maître qui chiffre toutes vos données avec AES-256 (PBKDF2 + AES-GCM). **Si vous perdez ce mot de passe, vos données locales sont irrécupérables** — exportez régulièrement.

### Export / Import
- **⬇ Exporter** : sauvegarde un fichier JSON lisible en clair
- **🔒 Chiffré** : sauvegarde un fichier JSON chiffré par mot de passe — partageable en toute sécurité
- **⬆ Importer** : restaure depuis un fichier JSON (chiffré ou non). Si chiffré, le mot de passe est demandé à l'ouverture

> 💡 En cas d'oubli du mot de passe, le bouton **Réinitialiser le chiffrement** sur l'écran de déverrouillage efface toutes les données locales et vous permet de repartir de zéro — ou de ré-importer une sauvegarde.

---

## 📊 Dashboard

Vue d'ensemble sur la période choisie (mois en cours, mois précédent, tout).

### KPIs affichés
- **Déficit total** : calories objectif − calories consommées sur la période
- **Perte estimée** : déficit total ÷ 7 700 kcal/kg
- **Poids théorique** : poids initial − perte calorique cumulée depuis le début
- **Dernière pesée** : dernier poids enregistré manuellement
- **Moy. calories** : moyenne journalière sur la période sélectionnée
- **Jours en déficit** : nombre de jours sous l'objectif calorique
- **Sport (période)** : distance totale des activités avec distance sur la période
- **J+30 (modèle Hall)** : projection réaliste à 30 jours avec adaptation métabolique

### Bannière objectif
Si un objectif de poids est défini, une bannière apparaît en haut du dashboard avec la progression en pourcentage, le déficit journalier nécessaire, les jours restants et un lien vers le détail. Elle disparaît automatiquement si la date limite est dépassée.

### Avertissement TDEE
Si les paramètres TDEE n'ont pas encore été configurés, un bandeau orange s'affiche avec un lien direct vers la configuration.

---

## 🎯 Objectifs

Définissez un objectif de poids avec une date limite. L'application calcule et affiche :

- **Perte ou prise totale** à accomplir (en kg), avec le point de départ et la cible
- **Jours restants** jusqu'à la date limite
- **Déficit journalier nécessaire** pour atteindre l'objectif dans les délais

### Faisabilité
L'objectif est évalué automatiquement selon le déficit nécessaire :
- ✓ **Réaliste** : déficit ≤ 600 kcal/j
- ⚠️ **Rythme agressif** : déficit entre 600 et 1 000 kcal/j
- ✗ **Risqué** : déficit > 1 000 kcal/j — un avertissement explicite s'affiche

### Progression
Une barre de progression indique le pourcentage accompli depuis le poids de départ vers la cible. En dessous, le **rythme actuel** est estimé depuis les 14 derniers jours de déficit réel, avec une projection de la date d'atteinte à ce rythme.

> 💡 Vous pouvez supprimer l'objectif à tout moment avec le bouton **Supprimer**.

---

## ⚖️ Poids

### Courbes
- **Courbe orange** : poids théorique basé sur les déficits caloriques depuis le début
- **Courbe bleue pointillée** : poids théorique étendu incluant les calories brûlées en sport
- **Modèle Hall** (violet) : projection réaliste avec adaptation métabolique (modèle NIH). Intègre le fait que le métabolisme ralentit progressivement au fur et à mesure de la perte de poids (−20 kcal/j par kg perdu), ce qui rend les projections à long terme plus fiables que le calcul linéaire simple
- **Fourchettes** optimiste/pessimiste : variation ±6–10% selon l'adhérence au déficit
- **Points verts** : pesées réelles enregistrées

### Enregistrer une pesée
Date + poids. L'écart par rapport au poids théorique s'affiche. Un ⚠️ rouge apparaît si la pesée dépasse le seuil théorique+sport, signalant un possible excès alimentaire non tracé ou une rétention d'eau.

### Projections
- **Actuel** : historique uniquement, sans extension dans le futur
- **J+30 / J+90 / J+180** : projection sur la durée choisie, toutes courbes prolongées

### Contrôles du graphique
Les boutons **+ zoom**, **− zoom** et **↺ reset** permettent de naviguer dans l'historique. Le bouton **👁 axe** bascule l'axe Y entre affichage relatif (variation autour du poids actuel) et absolu.

---

## 🧮 Calculateur

Recherche dans **1 356 aliments Ciqual** + vos références personnelles + vos recettes. Tapez au moins 2 lettres, saisissez le grammage, ajoutez à la liste. Le total calorique et les macronutriments (protéines, glucides, lipides, fibres) sont calculés automatiquement.

### Enregistrement
Cliquez **Enregistrer** pour sauvegarder la journée. Si une entrée existe déjà pour la date sélectionnée, les calories et macros sont **cumulées** (avec confirmation). Une note optionnelle peut être ajoutée à chaque journée.

### Mode édition
Cliquez sur une journée existante dans la liste pour passer en mode édition : les items de la journée sont rechargés dans le calculateur, et **Enregistrer** remplace l'entrée entière au lieu de l'additionner.

### Historique et tri
La liste des journées enregistrées est filtrable par texte et triable par date (ascendant/descendant) ou par calories.

---

## 📉 Déficit

Graphique en barres des apports caloriques journaliers vs l'objectif, filtrable par période (mois en cours, mois précédent, tout).

- **Barres vertes** : jours en déficit (sous l'objectif)
- **Barres rouges** : jours en surplus (au-dessus de l'objectif)

---

## 🥗 Nutriments

Suivi des macronutriments (protéines, glucides, lipides, fibres) par jour. Nécessite d'avoir utilisé le Calculateur avec des aliments renseignés en macros.

### Graphiques disponibles
- **Macros par jour** : barres empilées, filtrable par période
- **Évolution des macros** : courbes sur 30, 60, 90 jours ou tout l'historique, avec moyenne glissante sur 7 jours. Chaque macro est activable/désactivable individuellement via les boutons de légende

### Cibles journalières
Un bandeau affiche vos cibles calculées automatiquement depuis votre poids et votre objectif calorique :
- **Protéines** : 1,2–1,6 g/kg (consensus déficit calorique)
- **Lipides** : plancher ≥ 40 g/j (absorption des vitamines liposolubles)
- **Fibres** : ≥ 25 g/j (recommandation OMS)
- **Glucides** : pas de minimum physiologique établi — budget résiduel

Cliquez sur une barre du graphique pour voir la **composition détaillée du jour** avec la liste des aliments et leur contribution en kcal et macros.

---

## 📅 Bilan hebdo

Récapitulatif semaine par semaine : calories moyennes, déficit, macros vs cibles. La navigation entre semaines se fait via les boutons **< >** dans l'en-tête.

Un indicateur 📊 apparaît le dimanche pour signaler qu'un bilan de fin de semaine est disponible.

### Analyse automatique après 7 jours
Dès que vous avez au moins **7 jours de données enregistrées**, le bilan hebdo génère des **propositions personnalisées** pour la semaine suivante :

- ⚠️ **Protéines insuffisantes** : si votre moyenne est sous la cible — suggestions d'aliments (viandes, légumineuses, œufs) avec grammages indicatifs
- ⚠️ **Lipides trop bas** : si vous êtes sous le minimum recommandé — huile d'olive, noix, poisson gras
- ⚠️ **Fibres insuffisantes** : si vous êtes sous 25 g/j — légumes, légumineuses, céréales complètes
- 📈 **Glucides au-dessus du budget** : avec les aliments les plus contributeurs à réduire en priorité
- ✓ **Bonne semaine** : si tous les seuils sont respectés

> Ces seuils sont calculés depuis vos cibles nutritionnelles, elles-mêmes dérivées de vos paramètres TDEE.

---

## 📚 Références

Vos aliments personnalisés avec calories/100g et macros optionnelles. Apparaissent en priorité dans le Calculateur. Vous pouvez ajouter, modifier ou supprimer chaque référence. Une référence peut être créée directement depuis le Calculateur lors de la saisie d'un aliment.

---

## 🍲 Recettes

Créez des recettes en combinant plusieurs ingrédients de votre base Ciqual ou de vos références personnelles. Renseignez le poids total de la recette pour calculer automatiquement les valeurs nutritionnelles pour 100 g. La recette est ensuite ajoutée à vos références et disponible dans le Calculateur.

---

## 🔬 Données macro

Explorateur de la base Ciqual complète (1 356 aliments) avec filtres et tri par nutriment. Permet de comparer les aliments et de chercher des sources riches en un nutriment précis.

---

## 🏃 Sport

Visualisation de vos sessions sportives. Un **bloc de graphiques distinct est affiché pour chaque type d'activité** présent dans vos données : distance, durée, vitesse moyenne (si applicable), dépense calorique estimée. Filtrable par période (mois en cours, mois précédent, tout).

### ➕ Saisie sport

Enregistrez vos sessions : date, type d'activité, distance (si applicable), durée.

| Activité | MET | Distance |
|---|---|---|
| 🚴 Vélo intérieur | 4 | ✓ |
| 🚵 Vélo extérieur | 8 | ✓ |
| 🏃 Course à pied | 8 | ✓ |
| 🚶 Marche rapide | 4,5 | ✓ |
| 🏊 Natation | 7 | — |
| 🏋️ Musculation | 5 | — |
| ⚡ Autre | libre | — |

Pour l'activité **Autre**, le champ MET est éditable librement — utilisez un coefficient personnalisé (ex : 6 pour du yoga intensif, 10 pour du HIIT).

Les calories sont estimées via **MET × poids du jour × durée (h)**. Si aucune pesée n'existe avant la session, le poids de départ configuré dans TDEE est utilisé.

---

## ⚠️ À surveiller

Analyse automatique du **dernier bilan sanguin importé**. Les marqueurs sont classés en deux catégories :

- 🔴 **À surveiller** : marqueurs hors normes de référence sans explication contextuelle
- 🟢 **Connu / contextualisé** : marqueurs atypiques explicables par une condition chronique déclarée

### Conditions chroniques
Un panneau dépliable **🏥 Conditions chroniques** permet de déclarer vos pathologies connues (bêta-thalassémie, hypothyroïdie, diabète, insuffisance rénale, etc.). Une fois déclarée, chaque condition ajuste l'interprétation des marqueurs concernés dans l'analyse, les bilans sanguins détaillés et les rapports PDF. Les marqueurs concernés passent de "rouge" à "vert contextualisé".

---

## 🫀 Tension artérielle

Enregistrez vos mesures (systolique, diastolique, pouls optionnel). La zone OMS de chaque mesure est affichée :

- 🟢 **Optimale** : Sys < 120 et Dia < 80
- 🟡 **Normale** : Sys 120–129 et Dia ≤ 84
- 🟠 **Normale haute** : Sys 130–139 et Dia 85–89
- 🔴 **Hypertension G1** : Sys 140–159 ou Dia 90–99
- 🔴 **Hypertension G2** : Sys ≥ 160 ou Dia ≥ 100

Une **alerte automatique** s'affiche si la moyenne des 3 dernières mesures dépasse le seuil "Normale". Si une mesure existe déjà pour la même date, une confirmation de remplacement est demandée.

---

## 🩸 Bilans sanguins

Importez vos bilans au format JSON harmonisé. Les valeurs sont colorées selon leur statut (normal / bas / élevé), comparées bilan à bilan avec évolution en pourcentage, et regroupées par catégorie.

### Catégories de marqueurs disponibles
- 🔴 **Hématologie** : globules rouges, hémoglobine, hématocrite, MCV, MCH, MCHC, leucocytes, plaquettes
- 🧪 **Biochimie** : sodium, potassium, créatinine, eGFR, glucose, HbA1c, enzymes hépatiques (GOT, GPT, GGT), CK/CPK, CRP, sédimentation
- 💛 **Lipidique** : cholestérol total, HDL, LDL, VLDL, triglycérides, ratio CHOL/HDL (calculé automatiquement si absent)
- ⚙️ **Martial** : fer, ferritine
- ☀️ **Vitamines** : vitamine D
- 🔬 **Hormones** : TSH

### Tooltip explicatif
Survolez le nom de n'importe quel marqueur pour afficher sa définition, son organe cible et l'interprétation des valeurs hautes et basses.

### Export
Exportez vos bilans au format JSON pour les sauvegarder ou les partager indépendamment du reste de vos données.

---

## 🔥 Besoin journalier (TDEE)

Calcul de votre dépense énergétique totale via la formule **Mifflin-St Jeor × coefficient d'activité**. L'objectif calorique est recalculé automatiquement à chaque pesée enregistrée, en utilisant le dernier poids connu.

Paramètres configurables : sexe, âge, taille, poids, niveau d'activité. Ces valeurs alimentent également les calculs de projections de poids et les cibles nutritionnelles.

---

## 🔗 Corrélations

Analyse la relation entre vos marqueurs sanguins et vos données quotidiennes. Superpose l'évolution d'un marqueur biologique (sélectionnable via le menu) avec une métrique quotidienne au choix :

- **Déficit calorique** (kcal/j)
- **Apport calorique** (kcal/j)
- **Poids** (kg)

Les lignes verticales sur le graphique marquent les dates de bilan sanguin. Un lissage configurable (aucun, 7j, 14j, 30j) est disponible pour réduire le bruit des données quotidiennes. Un **mode test** peut être activé pour simuler des données et explorer l'interface sans données réelles.

---

## 📄 Rapports PDF

### 🩺 Rapport Santé
Destiné à votre médecin. Renseignez le nom du patient et le médecin destinataire (optionnel), sélectionnez les bilans à inclure. Le rapport contient :
- Conditions chroniques déclarées avec descriptions et marqueurs impactés
- Marqueurs hors norme avec interprétation clinique
- Marqueurs atypiques contextualisés par condition
- Tous vos bilans biologiques comparés côte à côte
- 5 dernières mesures de tension avec alerte si la moyenne dépasse le seuil

### 📊 Bilan Personnel
Vue d'ensemble de votre santé sur une période choisie (30j, 3 mois, 6 mois, tout l'historique). Les sections sont sélectionnables individuellement :
- ☑ **Poids & composition** : courbe de poids théorique et pesées réelles
- ☑ **Calories & déficit** : KPIs alimentaires, déficit cumulé, perte estimée
- ☑ **Vélo & sport** : distance, sorties, vitesse, calories brûlées
- ☑ **Marqueurs sanguins clés** : aperçu des valeurs biologiques importantes

---

## 🗑 Remise à zéro

Effaçage sélectif ou total des données, accessible depuis le bas de la sidebar.

### Par catégorie
Supprime uniquement les données d'un domaine, sans toucher aux autres :
- **🍽️ Repas & pesées** : historique journalier des calories, items, macros et pesées de poids
- **🏃 Sport** : toutes les sessions sportives enregistrées
- **🩺 Santé** : bilans sanguins, tension artérielle, snapshots hebdo
- **📚 Aliments** : références personnelles, recettes, historique d'usage

### Remise à zéro complète
Efface **absolument tout** sans exception. Un export avant cette opération est fortement recommandé.

---

## 💡 Conseils d'utilisation

- Pesez-vous **le matin à jeun** pour des mesures cohérentes et comparables
- Enregistrez vos calories chaque jour, même approximativement — la tendance compte plus que la précision absolue
- **Exportez régulièrement** vos données (export chiffré recommandé comme sauvegarde)
- Le poids théorique peut diverger de la réalité à cause de l'hydratation, du sel, du glycogène — c'est normal à court terme, la tendance sur 2–3 semaines est plus significative
- Si votre pesée dépasse le théorique+sport ⚠️, investiguez côté alimentation (sous-estimation des portions, repas non saisis)
- Utilisez le **modèle Hall** (violet) comme référence de projection long terme plutôt que la courbe orange linéaire — il tient compte du ralentissement métabolique
- Les suggestions du **Bilan hebdo** sont recalculées chaque semaine ; elles s'affinent au fur et à mesure que votre historique s'enrichit
