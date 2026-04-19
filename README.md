# 📊 Analyse du Marché de l'Emploi LinkedIn
![Aperçu du Dashboard](dashboard.png)
**Projet réalisé par Williams Ouattara & Zoran Doer**

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

## 🎨 Visualisations Streamlit
Le dashboard interactif permet d'explorer :
- **Top 10 Salaires & Volumes** : Visualisation par ID de secteur pour une performance optimale.
- 
- **Répartition par Taille** : Analyse des offres selon la dimension des entreprises.
- **Dictionnaire Dynamique (Sidebar)** : Pour pallier l'anonymisation des données, nous avons développé un moteur de recherche en barre latérale. L'utilisateur peut saisir un **ID technique** pour afficher instantanément le **Nom de l'entreprise** ou du **Secteur**.
 

## ⚠️ Problèmes rencontrés & Solutions
| Problèmes rencontrés | Solutions apportées |
| :--- | :--- |
| **Données anonymisées** (Graphiques remplis d'IDs peu lisibles). | Création d'un module de "Lookup" interactif dans la Sidebar pour traduire les IDs en temps réel. |
| **Incohérence de types** (IDs stockés en STRING vs NUMBER). | Utilisation systématique de `TRY_TO_NUMBER` et `CAST` dans les jointures pour éviter les erreurs de compilation. |
| **Données JSON complexes** | Utilisation des tables `RAW` avec colonne `VARIANT` pour isoler et extraire proprement les champs nécessaires. |

## 👥 Répartition équitable des tâches
- **Williams Ouattara** : Mise en place de l'environnement Snowflake, création des scripts ETL (`linkedin.sql`), nettoyage des données et logique de jointure complexe.
- **Zoran Doer** : Développement de l'interface Streamlit (`streamlit_app.py`), conception du dictionnaire d'identifiants et rédaction de la documentation technique.

---
*Projet réalisé dans le cadre de la formation Data. Les données utilisées proviennent d'un échantillon représentatif du marché de l'emploi LinkedIn.*
