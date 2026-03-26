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

Au premier lancement, vous choisissez un mot de passe maître qui chiffre toutes vos données avec **AES-256-GCM + PBKDF2-SHA-256 (200 000 itérations)**. **Si vous perdez ce mot de passe, vos données locales sont irrécupérables** — exportez régulièrement.

Le schéma de chiffrement est **versionné** : chaque blob chiffré embarque sa version cryptographique (`v`, `algo`, paramètres). Cela garantit que vos données resteront déchiffrables même si les paramètres évoluent dans une future version de l'application — aucune migration manuelle ne sera nécessaire.

### Export / Import

- **⬇ Exporter** : sauvegarde un fichier JSON lisible en clair
- **🔒 Chiffré** : sauvegarde un fichier JSON chiffré par mot de passe — partageable en toute sécurité. Le fichier chiffré embarque également la version du schéma crypto pour garantir la compatibilité future
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

> **Source :** Academy of Nutrition and Dietetics — un déficit supérieur à 1 000 kcal/j augmente le risque de perte musculaire et de carences nutritionnelles. Un rythme de 0,5–1 kg/semaine est considéré comme sûr et durable.

### Progression

Une barre de progression indique le pourcentage accompli depuis le poids de départ vers la cible. En dessous, le **rythme actuel** est estimé depuis les 14 derniers jours de déficit réel, avec une projection de la date d'atteinte à ce rythme.

> 💡 Vous pouvez supprimer l'objectif à tout moment avec le bouton **Supprimer**.

---

## ⚖️ Poids

### Courbes

- **Courbe orange** : poids théorique basé sur les déficits caloriques depuis le début (modèle linéaire 7 700 kcal/kg)
- **Modèle Hall** (violet) : projection réaliste avec adaptation métabolique (modèle NIH). Intègre le fait que le métabolisme ralentit progressivement au fur et à mesure de la perte de poids (−20 kcal/j par kg perdu), ce qui rend les projections à long terme plus fiables que le calcul linéaire simple
- **Fourchettes** optimiste/pessimiste : variation ±6–10% selon l'adhérence au déficit
- **Points verts** : pesées réelles enregistrées

> **Sources :**
> - Constante 7 700 kcal/kg : valeur physiologique de référence largement utilisée en clinique, fondée sur la composition du tissu adipeux (≈ 87 % de lipides × 9 kcal/g).
> - Modèle Hall : *Hall KD et al. (2011). "Quantification of the effect of energy imbalance on bodyweight." The Lancet, 378(9793), 826–837.* Le modèle intègre l'adaptation métabolique et la perte de masse maigre, absentes du calcul linéaire simple.

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

> **Source Ciqual :** Table de composition nutritionnelle des aliments du Centre de Recherche pour l'Étude et l'Observation des Conditions de Vie (CREDOC) / Anses. [https://ciqual.anses.fr](https://ciqual.anses.fr)

### Sélecteur de repas

Chaque aliment ajouté peut être assigné à un moment de la journée via les boutons :

- 🌅 **Petit déjeuner**
- ☀️ **Déjeuner**
- 🍎 **En-cas**
- 🌙 **Dîner**

Cette répartition est utilisée dans le **Bilan hebdo** pour l'analyse chrono-nutritionnelle (voir ci-dessous).

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

> **Sources :**
> - Protéines en déficit : *Helms ER et al. (2014). "Evidence-based recommendations for natural bodybuilding contest preparation." Journal of the International Society of Sports Nutrition, 11(1), 20.* Fourchette 1,2–2,2 g/kg selon l'intensité de l'entraînement.
> - Lipides minimum : *Lichtenstein AH et al. (2006). AHA Dietary Guidelines. Circulation.* Un apport inférieur à 20% des calories compromet l'absorption des vitamines A, D, E, K.
> - Fibres OMS : *World Health Organization (2003). Diet, Nutrition and the Prevention of Chronic Diseases. WHO Technical Report Series 916.* Cible ≥ 25 g/j pour adulte.

Cliquez sur une barre du graphique pour voir la **composition détaillée du jour** avec la liste des aliments et leur contribution en kcal et macros.

---

## 📅 Bilan hebdo

Récapitulatif semaine par semaine : calories moyennes, déficit, macros vs cibles. La navigation entre semaines se fait via les boutons **< >** dans l'en-tête. Les semaines complètes (7 jours) sont snapshotées et consultables dans l'historique.

Un indicateur 📊 apparaît quand un bilan de semaine complète est disponible.

### Analyse macronutriments

Après au moins **3 jours de données**, le bilan génère des **propositions personnalisées** :

- ⚠️ **Protéines insuffisantes** : si votre moyenne est sous la cible — suggestions d'aliments (viandes, légumineuses, œufs) avec grammages indicatifs
- ⚠️ **Lipides trop bas** : si vous êtes sous le minimum recommandé — huile d'olive, noix, poisson gras
- ⚠️ **Fibres insuffisantes** : si vous êtes sous 25 g/j — légumes, légumineuses, céréales complètes
- 📈 **Glucides au-dessus du budget** : avec les aliments les plus contributeurs à réduire en priorité
- ✓ **Bonne semaine** : si tous les seuils sont respectés

> Ces seuils sont calculés depuis vos cibles nutritionnelles, elles-mêmes dérivées de vos paramètres TDEE.

### ⏰ Répartition chrono-nutritionnelle

Si vous avez utilisé le **sélecteur de repas** dans le Calculateur, un bloc supplémentaire apparaît dans le bilan hebdo avec l'analyse de votre répartition calorique et nutritionnelle selon le moment de la journée.

**Ce qui est affiché :**

- Barre visuelle de répartition des calories entre Petit déjeuner / Déjeuner / En-cas / Dîner
- Pour chaque repas : % des kcal journalières vs la cible recommandée, écart en vert/orange/rouge
- Répartition des protéines, glucides, lipides entre les repas

**Cibles recommandées (% des kcal journalières) :**

| Repas | Cible | Rôle |
|---|---|---|
| 🌅 Petit déjeuner | 25 % | Activation du métabolisme, satiété matinale |
| ☀️ Déjeuner | 40 % | Repas principal, pic thermique de la journée |
| 🍎 En-cas | 5 % | Régulation de la glycémie entre les repas |
| 🌙 Dîner | 30 % | Repas de récupération, limiter les glucides simples |

**Observations automatiques générées :**

- 🌙 Dîner trop lourd calorique par rapport au déjeuner
- 🥚 Apport protéique insuffisant au petit déjeuner
- ⚠️ Protéines trop concentrées sur le dîner
- 🌅 Petit déjeuner trop léger ou absent
- ✅ Confirmations si la répartition est conforme

> **Sources (chrono-nutrition) :**
> - *Garaulet M & Gómez-Abellán P (2014). "Timing of food intake and obesity: a novel association." Physiology & Behavior, 134, 44–50.* Les calories consommées le matin sont associées à une meilleure perte de poids que les mêmes calories consommées le soir.
> - *Jakubowicz D et al. (2013). "High caloric intake at breakfast vs. dinner differentially influences weight loss in overweight and obese women." Obesity, 21(12), 2504–2512.* Un petit déjeuner riche et un dîner léger favorisent la perte de poids et améliorent la glycémie.
> - *Leidy HJ et al. (2015). "The role of protein in weight loss and maintenance." AJCN, 101(6), 1320S–1329S.* Un apport protéique au petit déjeuner réduit l'appétit et les fringales dans la journée.
> - *PNNS (Programme National Nutrition Santé, France).* Répartition indicative : petit déjeuner 20–25 %, déjeuner 35–40 %, dîner 25–30 %, en-cas 5–10 %.
> - Ces cibles sont **indicatives et non contractuelles**. Des stratégies comme le jeûne intermittent (absence de petit déjeuner volontaire) peuvent être parfaitement valides selon les objectifs individuels.

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

> **Source MET :** *Ainsworth BE et al. (2011). "2011 Compendium of Physical Activities." Medicine & Science in Sports & Exercise, 43(8), 1575–1581.* Le MET (Metabolic Equivalent of Task) exprime l'intensité d'une activité par rapport au métabolisme de repos (1 MET = 1 kcal/kg/h).

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

> **Source :** *Williams B et al. (2018). "2018 ESC/ESH Guidelines for the management of arterial hypertension." European Heart Journal, 39(33), 3021–3104.* Classification adoptée par l'OMS et l'ESH (European Society of Hypertension).

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

### Formule Mifflin-St Jeor

```
Homme : MB = (10 × poids) + (6,25 × taille) − (5 × âge) + 5
Femme : MB = (10 × poids) + (6,25 × taille) − (5 × âge) − 161
TDEE  = MB × coefficient d'activité
```

> **Source :** *Mifflin MD et al. (1990). "A new predictive equation for resting energy expenditure in healthy individuals." American Journal of Clinical Nutrition, 51(2), 241–247.* Considérée comme la formule la plus précise pour les individus sédentaires à modérément actifs, avec une marge d'erreur de ±10% sur la population générale.

### Scénarios caloriques

| Scénario | Multiplicateur | Variation poids estimée |
|---|---|---|
| Prise de masse | TDEE × 1,10 | +0,22 kg/sem environ |
| Maintien | TDEE × 1,00 | 0 |
| Perte légère | TDEE × 0,90 | −0,22 kg/sem environ |
| Perte modérée | TDEE × 0,80 | −0,44 kg/sem environ |
| Perte rapide | TDEE × 0,75 | −0,56 kg/sem environ |

> La variation de poids est estimée à partir du surplus ou déficit calorique journalier × 7 jours ÷ 7 700 kcal/kg. Ces valeurs sont des estimations — la réalité varie selon la masse musculaire, l'hydratation et l'adaptation métabolique.

Le bouton **Utiliser comme objectif** applique directement le scénario sélectionné comme objectif calorique journalier.

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
- **Exportez régulièrement** vos données (export chiffré recommandé comme sauvegarde principale)
- Le poids théorique peut diverger de la réalité à cause de l'hydratation, du sel, du glycogène — c'est normal à court terme, la tendance sur 2–3 semaines est plus significative
- Si votre pesée dépasse le théorique+sport ⚠️, investiguez côté alimentation (sous-estimation des portions, repas non saisis)
- Utilisez le **modèle Hall** (violet) comme référence de projection long terme plutôt que la courbe orange linéaire — il tient compte du ralentissement métabolique
- Les suggestions du **Bilan hebdo** sont recalculées chaque semaine ; elles s'affinent au fur et à mesure que votre historique s'enrichit
- Pour profiter de l'analyse **chrono-nutritionnelle**, pensez à assigner chaque aliment à son repas dans le Calculateur via les boutons 🌅 ☀️ 🍎 🌙

---

## 📖 Références scientifiques complètes

### Métabolisme & dépense énergétique

- **Mifflin MD et al. (1990).** "A new predictive equation for resting energy expenditure in healthy individuals." *American Journal of Clinical Nutrition*, 51(2), 241–247.
- **Harris JA & Benedict FG (1918).** "A Biometric Study of Human Basal Metabolism." *Proceedings of the National Academy of Sciences*, 4(12), 370–373. *(formule historique, supplantée par Mifflin)*
- **Ainsworth BE et al. (2011).** "2011 Compendium of Physical Activities." *Medicine & Science in Sports & Exercise*, 43(8), 1575–1581. *(coefficients MET)*

### Poids & composition corporelle

- **Hall KD et al. (2011).** "Quantification of the effect of energy imbalance on bodyweight." *The Lancet*, 378(9793), 826–837. *(modèle Hall — adaptation métabolique)*
- **Hall KD (2008).** "What is the required energy deficit per unit weight loss?" *International Journal of Obesity*, 32(3), 573–576. *(constante 7 700 kcal/kg)*

### Macronutriments & cibles nutritionnelles

- **Helms ER et al. (2014).** "Evidence-based recommendations for natural bodybuilding contest preparation." *Journal of the International Society of Sports Nutrition*, 11(1), 20. *(protéines en déficit)*
- **Leidy HJ et al. (2015).** "The role of protein in weight loss and maintenance." *American Journal of Clinical Nutrition*, 101(6), 1320S–1329S.
- **Lichtenstein AH et al. (2006).** AHA Dietary Guidelines. *Circulation*, 114(1), 82–96. *(lipides minimum)*
- **World Health Organization (2003).** *Diet, Nutrition and the Prevention of Chronic Diseases.* WHO Technical Report Series 916. *(fibres ≥ 25 g/j)*

### Chrono-nutrition & répartition des repas

- **Garaulet M & Gómez-Abellán P (2014).** "Timing of food intake and obesity: a novel association." *Physiology & Behavior*, 134, 44–50.
- **Jakubowicz D et al. (2013).** "High caloric intake at breakfast vs. dinner differentially influences weight loss." *Obesity*, 21(12), 2504–2512.
- **Leidy HJ et al. (2015).** "The role of protein in weight loss and maintenance." *AJCN*, 101(6), 1320S–1329S. *(protéines au petit déjeuner)*
- **PNNS — Programme National Nutrition Santé (France).** Recommandations sur la répartition des repas. [https://www.mangerbouger.fr](https://www.mangerbouger.fr)

### Cardiologie & tension artérielle

- **Williams B et al. (2018).** "2018 ESC/ESH Guidelines for the management of arterial hypertension." *European Heart Journal*, 39(33), 3021–3104.

### Données alimentaires

- **Anses — Agence nationale de sécurité sanitaire (2020).** Table Ciqual de composition nutritionnelle des aliments. [https://ciqual.anses.fr](https://ciqual.anses.fr)

---

> *Ces informations ont une visée éducative et ne constituent pas un avis médical. Consultez un professionnel de santé pour tout suivi médical ou nutritionnel personnalisé.*
