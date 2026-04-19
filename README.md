# 📊 Analyse du Marché de l'Emploi LinkedIn
**Projet réalisé par Williams Ouattara & Zoran Doerr**

## 📝 Présentation du projet
Ce projet consiste en une analyse approfondie d'un dataset LinkedIn utilisant l'écosystème **Snowflake** pour le stockage et le traitement, et **Streamlit** pour la visualisation interactive. L'objectif est d'extraire des tendances significatives sur les salaires, les secteurs d'activité et les types de contrats.

## 📂 Structure du Dépôt
- `linkedin.sql` : Script ETL (Configuration, création des stages S3, chargement des fichiers CSV/JSON et nettoyage initial).
- `A_linkedin.sql` : Analyses SQL avancées (Ranking, statistiques salariales et transformations métier).
- `streamlit_app.py` : Code source de l'application interactive développée sous Streamlit in Snowflake.
- `requirements.txt` : Dépendances Python nécessaires au projet.

## 🛠️ Méthodologie & Commandes SQL
Nous avons mis en place un pipeline de données robuste :
1. **Extraction (Stage S3)** : Récupération des données brutes depuis un bucket AWS S3.
2. **Parsing JSON** : Utilisation de la syntaxe Snowflake (`v:industry::STRING`) pour aplatir les données semi-structurées des entreprises et industries.
3. **Jointures Techniques** : Utilisation de `TRY_TO_NUMBER()` pour lier les offres d'emploi (contenant des IDs en texte) aux tables de référence des entreprises.
4. **Calculs Statistiques** : Utilisation de fonctions d'agrégation et de fenêtrage (`RANK() OVER`) pour identifier les top métiers par secteur.

## 🎨 Visualisations & Dashboard Interactif

Le dashboard a été conçu pour offrir une double lecture : une analyse statistique globale et un outil de forage (drill-down) individuel.

#### 1. Analyse des Secteurs et Rémunérations
Nous avons corrélé le volume d'offres avec les salaires moyens pour identifier les secteurs les plus porteurs. L'affichage par ID garantit une fluidité de navigation même sur de gros volumes de données.
![Analyses secteurs et salaires](https://github.com/user-attachments/assets/f31d0859-5592-4376-af2f-744a13a6db8f)

#### 2. Structure des Entreprises et Métiers
Cette section permet d'observer la typologie des recruteurs (TPE, PME ou Grands Groupes) ainsi que le top 10 des intitulés de postes les plus recherchés.
![Répartitions entreprises et titres](https://github.com/user-attachments/assets/3d647de7-628a-44e7-b3af-69438dfff9eb)

#### 3. Typologie des Contrats
Une vue synthétique traduite en français pour une meilleure compréhension des modes de travail prédominants sur le marché.
![Typologie des contrats](https://github.com/user-attachments/assets/ab6d29d1-fa88-4418-81d9-a61c721a9f04)

#### 4. Dictionnaire Dynamique (Sidebar)
Face à l'anonymisation des données par IDs, nous avons intégré un **moteur de recherche intelligent** en barre latérale. Cet outil permet à l'utilisateur de "décoder" instantanément n'importe quel ID technique en nom réel (Entreprise ou Industrie).


![Traducteur d'identifiants](https://github.com/user-attachments/assets/306ed867-a932-4083-8b65-aa1a9e9b2e28)

## ⚠️ Problèmes rencontrés & Solutions
| Problèmes rencontrés | Solutions apportées |
| :--- | :--- |
| **Données anonymisées** | Création d'un module de "Lookup" interactif dans la Sidebar pour traduire les IDs en temps réel. |
| **Incohérence de types** | Utilisation systématique de `TRY_TO_NUMBER` et `CAST` dans les jointures pour éviter les erreurs de compilation. |
| **Données JSON complexes** | Utilisation des tables `RAW` avec colonne `VARIANT` pour isoler et extraire proprement les champs nécessaires. |

## 👥 Répartition équitable des tâches
- **Williams Ouattara** : Mise en place de l'environnement Snowflake, création des scripts ETL (`linkedin.sql`), nettoyage des données et logique de jointure complexe.
- **Zoran Doerr** : Développement de l'interface Streamlit (`streamlit_app.py`), conception du dictionnaire d'identifiants et rédaction de la documentation technique.

---
*Projet réalisé dans le cadre de la formation Data. Williams Ouattara & Zoran Doer.*
