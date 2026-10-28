# Projet BI - Analyse et détection d’anomalies

Ce projet structure un pipeline de traitement de données Power BI en plusieurs étapes, orchestrées via un graphe LangGraph.

## Objectif

Le projet lit un fichier Power BI (`data/finalbi.pbix`), extrait les tables utiles, calcule des KPI mensuels, détecte les anomalies, explique les causes, produit un rapport HTML et prépare des insights exportables pour Power BI.

## Architecture

```text
projet_bi/
├── data/
│   ├── finalbi.pbix
│   ├── FactSales.csv
│   ├── DimProduct.csv
│   ├── DimSalesTerritory.csv
│   └── DimDate.csv
├── agents/
│   ├── __init__.py
│   ├── extract.py
│   ├── kpi.py
│   ├── detect.py
│   ├── analyse.py
│   ├── write.py
│   ├── validate.py
│   └── report.py
├── output/
│   ├── kpi_mensuels.csv
│   ├── alertes.csv
│   ├── agent_insights.csv
│   └── rapport_complet.html
├── tests/
│   ├── test_kpi.py
│   └── test_validate.py
├── .env
├── config.py
├── graph.py
├── main.py
├── requirements.txt
├── LISEZMOI.md
└── .venv/
```

## Rôle des dossiers

### `data/`
Contient les fichiers source et les exportations CSV produites depuis le modèle Power BI.

### `agents/`
Chaque fichier correspond à un nœud du graphe LangGraph.

- `extract.py` : extraction du modèle Power BI avec `pbixray`
- `kpi.py` : calcul des indicateurs KPI mensuels
- `detect.py` : détection des anomalies et écarts
- `analyse.py` : expliquation des causes (prix, volume, mix)
- `write.py` : génération des narrations avec Groq
- `validate.py` : contrôle de cohérence des résultats
- `report.py` : génération du rapport HTML/CSV final

### `output/`
Dossier des résultats produits par le pipeline.

### `tests/`
Tests unitaires de validation métier ; par exemple, la vérification d’un KPI mensuel attendu.

## Variables d’environnement

Un fichier `.env` doit contenir au minimum :

```env
GROQ_API_KEY="votre_cle_groq"
```

Ne jamais publier cette clé dans le dépôt.

## Installation

```powershell
cd D:\BI\projet_bi
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Lancement

```powershell
cd D:\BI\projet_bi
python main.py
```

## Bonnes pratiques

- Garder les agents indépendants et orientés fonction.
- Produire les sorties dans `output/` pour faciliter les validations.
- Vérifier les chiffres dans `validate.py` avant la publication du rapport final.
- S’assurer que les colonnes Power BI sont normalisées avant les calculs.

## Étapes prévues du pipeline

1. Extraction de données PBIX
2. Calcul des KPI mensuels
3. Détection d’anomalies
4. Analyse de causes
5. Génération de narration
6. Validation des chiffres
7. Production du rapport final

## Remarque

Les fichiers Python ci-dessus constituent la structure de base du projet. Les agents peuvent ensuite être enrichis pour refléter précisément la logique métier de votre modèle Power BI.
