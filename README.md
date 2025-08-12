# 📊 Tableau de Bord Power BI - Analyse P&L Multi-Entités

## 🎯 Contexte du Projet

**Mission :** Développement d'un tableau de bord Power BI pour l'analyse des performances financières d'un groupe du CAC 40  
**Périmètre :** 8 Business Units réparties sur 17 pays (données 2018-2020)  
**Objectif :** Transformer les données financières complexes en insights actionnables pour le pilotage du groupe

### Problématiques Métier Adressées
- Quelle est la performance de nos meilleures et pires filiales ?
- Comment se comparent nos résultats réels aux prévisionnels ?
- Quelles sont les évolutions par rapport aux années précédentes ?
- Où concentrer nos efforts d'optimisation géographique ?

## 🏗️ Architecture Technique

### Modèle de Données
**Architecture Étoile :**
- **Table de Faits :** `Depense` - Transactions financières consolidées (15K+ lignes)
- **Dimensions :**
  - `Entity` : Business Units et géographie (Pays/Continents - 17 pays)
  - `Compte` : Plan comptable hiérarchique (LEV1 à LEV4)
  - `Calendrier` : Dimension temporelle complète (2018-2020)
  - `PHASE` : Scénarios (Budget, Réalisé, Prévisions)

**Relations Implémentées :**
- Depense → Entity (1:N via ID_ENTITY)
- Depense → Compte (1:N via ID_ACCOUNT) 
- Depense → Calendrier (1:N via Date)
- Depense → PHASE (1:N via ID_PHASE)

### Sources de Données
- `Fact_table.xlsx` : Données de consolidation financière (table Depense)
- `Entity_Country.xlsx` : Référentiel entités et pays (table Entity)
- `Structure_Comptes.xlsx` : Plan comptable hiérarchique (table Compte)

### Mesures DAX Développées

**Indicateurs de Performance Principaux :**
- **Budget** : Montant budgétaire par entité/compte
- **Conso** : Consommation réelle (réalisé)
- **Conso Y-1** : Consommation année précédente
- **conso-Budget** : Écart absolu réalisé vs budget
- **Conso/Budget** : Ratio de performance budgétaire

**Ratios et Comparaisons :**
- **Ratio Conso vs Budget** : Pourcentage de réalisation du budget
- **Budget MoM%** : Évolution mensuelle du budget
- **Conso MoM%** : Évolution mensuelle de la consommation
- **Ratio_Conso** : Autres ratios de performance

**Hiérarchies et Sélecteurs :**
- **Table_Titres** : Filtres dynamiques (Select_Month, Select_Year, SelectContinent)
- **Titre Business Unit** : Sélecteur Business Unit contextuel
- Hiérarchies : Business Unit, LABEL_ACC (LEV1-LEV4), géographique

## 📋 Pages du Tableau de Bord

### 1. 🏠 Page d'Accueil - Vue Synthétique
**Indicateurs Clés :**
- **Résultat Consolidé :** 220K€
- **Performance vs N-1 :** +24% (177K€ → 220K€)
- **Performance vs Budget :** +98% (111K€ → 220K€)

**Analyse P&L Détaillée :**
- Marge Brute : 673K€ (+13% vs N-1)
- Frais SG&A : -410K€ 
- Résultat Net : 220K€

**Points d'Attention Identifiés :**
- Frais d'Intérêt Net : +1149% vs Budget (39K€ vs 3K€ prévu)
- Coûts Exceptionnels : +49% vs Budget
- Écart de Change : Impact défavorable

### 2. 💼 Analyse Business Unit
**Top 5 des BU Performantes :**
1. **PASIA :** 87K€ (croissance exceptionnelle 2018-2020)
2. **HOLDINGFR :** 50K€ (performance stable)
3. **AMERICA19 :** 46K€ (progression régulière)
4. **MASSWW :** 9K€ (redressement en cours)
5. **PEUROPE19 :** 30K€ (tendance décroissante)

**Évolution Temporelle :**
- 2018 : 74K€
- 2019 : 103K€ (pic de performance)
- 2020 : 43K€ (impact COVID-19)

### 3. 🗺️ Analyse Géographique
**Cartographie Interactive :**
- Visualisation budget et consommation par continent
- Cartes intégrées TomTom/Microsoft
- Filtrage dynamique par zones géographiques

### 4. 🌍 Analyse par Pays
**Top Pays Contributeurs :**
1. **Hong-Kong :** 61K€ (28% du résultat total)
2. **France :** 55K€ (25% du résultat total)
3. **États-Unis :** 41K€ (19% du résultat total)
4. **Portugal :** 18K€

**Pays à Surveiller :**
- Irlande : -8K€ (performance négative)
- RDC : -4K€ (difficultés opérationnelles)
- Japon : -4K€ (marché en restructuration)

## 🛠️ Technologies Utilisées

- **Power BI Desktop :** Développement et modélisation
- **Power Query :** Transformation et nettoyage des données
- **DAX :** Calculs avancés et intelligence temporelle
- **Excel :** Sources de données et validation
- **Power BI Service :** Déploiement et partage (prévu)

## 📊 Fonctionnalités Implémentées

### Navigation et Filtrage
- **Menu de Navigation :** Accès rapide entre les 4 pages principales
- **Filtres Contextuels :** Continent/Pays, Business Unit, Année/Mois
- **Interactions Croisées :** Filtrage dynamique entre visualisations

### Visualisations Métier
- **Tableaux Croisés Dynamiques :** P&L mensuel avec drill-down
- **Graphiques en Barres :** Performance Business Units
- **Cartes Géographiques :** Analyse spatiale des performances
- **Graphiques Temporels :** Évolutions sur 3 ans

### Indicateurs de Performance
- **Comparaisons Multiples :** Réalisé vs Budget vs N-1
- **Calculs de Variance :** Écarts absolus et relatifs
- **Ratios Financiers :** Marges et performances relatives

## 📁 Structure du Repository

```
📦 PowerBI-Financial-Dashboard/
├── 📊 Reports/
│   ├── PowerBI_Financial_Dashboard.pbix       # Fichier Power BI principal
│   └── Data_Model_Schema.png                  # Schéma du modèle relationnel
├── 📁 Data_Sources/
│   ├── Fact_table.xlsx                        # Table de faits Depense
│   ├── Entity_Country.xlsx                    # Dimension Entity/Country
│   ├── Structure_Comptes.xlsx                 # Dimension Compte hiérarchique
│   └── Table_Phase_Calendrier.xlsx            # Dimensions PHASE et Calendrier
├── 📸 Screenshots/
│   ├── 01_Accueil_Vue_Synthetique.png
│   ├── 02_Analyse_Business_Unit.png
│   ├── 03_Analyse_Geographique.png
│   └── 04_Analyse_par_Pays.png
├── 📋 docs/
│   ├── Specifications_Techniques.md       # Détail des mesures DAX
│   ├── Guide_Utilisateur.pdf              # Mode d'emploi du dashboard
│   └── Cahier_des_Charges.md              # Requirements originaux

```

## 🎯 Insights Business Générés

### Performance Globale
> **Résultat exceptionnel :** Le groupe dépasse largement ses objectifs avec 220K€ de résultat, soit +98% vs budget initial. Cette surperformance s'explique principalement par l'excellence de la région PASIA.

### Analyse Géographique
> **Concentration des risques :** 71% du résultat provient de seulement 3 pays (Hong-Kong, France, USA). Une stratégie de diversification géographique pourrait réduire cette dépendance.

### Business Units
> **PASIA : Star Performer :** Avec 87K€ de contribution, cette BU représente 40% du résultat total et montre une croissance constante sur 3 ans.

### Points d'Alerte
> **Dérapage des coûts financiers :** +1149% vs budget nécessite une action immédiate de l'équipe finance pour comprendre et corriger cette dérive.

## 📈 Évolution Prévue - Roadmap V2

### Fonctionnalités en Développement
- 🔮 **Analyses Prédictives :** Forecasting 6 mois avec intervalles de confiance
- 📊 **Visualisations Avancées :** Waterfall charts pour analyse des variances
- ⚡ **Alertes Temps Réel :** Notifications sur dépassements de seuils
- 📱 **Optimisation Mobile :** Interface responsive pour dirigeants

### Valeur Ajoutée V2
- **Scénarios What-If :** Simulation d'impact des décisions stratégiques
- **Benchmarking :** Comparaisons sectorielles et ratios de référence
- **Automatisation :** Refresh automatique et reporting programmé

## 🚀 Démo et Captures d'Écran

### Vue d'Ensemble - Page d'Accueil
![Page d'Accueil](screenshots/01_Accueil_Vue_Synthetique.png)
*Tableau de bord exécutif avec KPIs consolidés et alertes visuelles*

### Analyse Business Unit
![Business Units](screenshots/02_Analyse_Business_Unit.png)
*Performance comparative des 8 Business Units avec évolutions temporelles*

### Cartographie des Performances
![Analyse Géographique](screenshots/03_Analyse_Geographique.png)
*Visualisation géographique interactive des budgets et réalisations*

### Détail par Pays
![Analyse par Pays](screenshots/04_Analyse_par_Pays.png)
*Tableau détaillé des contributions par pays avec classement*

## 🎥 Démonstration Vidéo

[![Démo Power BI Dashboard](https://img.youtube.com/vi/YOUR_VIDEO_ID/0.jpg)](https://youtu.be/YOUR_VIDEO_ID)

**Durée :** 3 minutes | **Contenu :** Navigation complète et présentation des insights clés

## 🔗 Liens Utiles

- **📊 Dashboard Interactif :** [Power BI Service](lien-vers-powerbi-service) *(Accès sur demande)*
- **💼 Portfolio Complet :** [LinkedIn - Ésaïe Daniel LUPEPÉLÉ](https://www.linkedin.com/in/esaie-lupepele)
- **🔧 Autres Projets :** [Mapping Infor M3](https://github.com/LouspDan/Mapping-Infor-M3)
- **📧 Contact Projet :** esaie.lupepele@gmail.com

## 📄 Méthodologie et Apprentissages

### Approche de Développement
1. **Analyse des Besoins :** Identification des KPIs métier prioritaires
2. **Modélisation :** Architecture en étoile optimisée pour les performances
3. **Développement Itératif :** 4 pages développées selon priorités utilisateur
4. **Tests et Validation :** Vérification cohérence données et calculs

### Défis Techniques Surmontés
- **Données Multi-Sources :** Consolidation et réconciliation des référentiels
- **Calculs Complexes :** Time Intelligence et comparaisons multi-périodes  
- **Performance :** Optimisation temps de chargement pour gros volumes
- **UX/UI :** Design cohérent et navigation intuitive

### Compétences Démontrées
- ✅ **Analyse Financière :** Compréhension des enjeux P&L groupe
- ✅ **Modélisation BI :** Architecture de données scalable (10+ ans d'expérience)
- ✅ **DAX Avancé :** Mesures complexes et intelligence temporelle
- ✅ **Design UX :** Interface utilisateur métier-oriented
- ✅ **Gouvernance Data :** Standards de qualité et documentation (expérience Hermès)

## 📊 Métriques du Projet

- **⏱️ Temps de Développement :** 3 semaines (60h)
- **📏 Complexité Technique :** 25+ mesures DAX, 4 dimensions, 15K+ lignes
- **👥 Impact Utilisateurs :** Dashboard multi-profils (Executives, Controllers, Analysts)
- **🎯 Valeur Business :** Identification 3M€ d'optimisations potentielles

---

## 🏷️ Tags

`#PowerBI` `#BusinessIntelligence` `#Analyse-Financière` `#Dashboard` `#DAX` `#Visualisation-Données` `#P&L` `#CAC40` `#Multi-Entités` `#Portfolio`

---

### 📝 Notes

- **Données :** Entièrement anonymisées et à des fins de démonstration
- **Contexte :** Projet développé dans le cadre d'un cas d'étude réaliste
- **Évolution :** Version 2.0 en développement avec fonctionnalités avancées

**Disponible pour projets similaires et missions BI/Data Analytics**