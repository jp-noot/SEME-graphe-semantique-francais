# Graphe de sémantique de la langue française

Projet réalisé lors de la **SEME (Semaine d'Études Maths-Entreprises)**, Marseille, novembre 2023.
Objectif : construire un graphe sémantique du français (mots et relations entre mots) à partir de
ressources lexicales et de modèles de langue.

## Contenu

| Élément | Description |
|---|---|
| `notebooks/01_wordnet_nltk` | Prise en main de WordNet (NLTK, OMW) pour le français |
| `notebooks/02_construction_table` | Table `mot_fr / synset / mot_en / nature` à partir de `data/data_toyes.txt` |
| `notebooks/03_pipeline_graphe` | Pipeline principal : définitions WordNet, embeddings CamemBERT, similarités, graphe `networkx` |
| `notebooks/04_synonymes_wolf` | Reconstruction de synonymes avec WOLF (adapté d'un TD de Xavier Dupré, voir le notebook) |
| `notebooks/exploration/` | Essais préparatoires : exploration de CamemBERT (adapté d'un tutoriel de blog) et de Lexique383 |
| `data/` | Jeu de données jouet (mots fréquents) |
| `figures/` | Graphes obtenus (`graphe_finale.pdf` est régénéré par `03_pipeline_graphe` ; `graphe_finale_v2.pdf` date de 2023) |
| `rapport/` | `rapport_final.pdf` (synthèse), sources LaTeX (`Synthese.tex`, `main.tex` pour la présentation beamer), présentation `.pptx` |

## Méthode et résultats

Chaque **concept** est une définition WordNet (traduite en français) ; deux concepts sont reliés lorsque la similarité cosinus de leurs représentations CamemBERT (moyenne des vecteurs de tokens) dépasse **0,8**. Sur les mots « orange » et « voiture » (14 concepts), le graphe a deux composantes connexes : 12 concepts liés entre eux, et 2 concepts liés à la géographie de l'Afrique du Sud. Détails, limites et pistes d'amélioration (dictionnaire français plutôt que traduction, choix du seuil, fine-tuning de CamemBERT) : voir `rapport/rapport_final.pdf`.

## Références

- L. Martin et al., *CamemBERT: a Tasty French Language Model*, ACL 2020.
- C. Fellbaum, *WordNet*, in *Theory and applications of ontology: computer applications*, Springer, 2010 ; E. Loper et S. Bird, *NLTK: the Natural Language Toolkit*, 2002.
- B. Sagot et D. Fišer, *Building a free French wordnet from multilingual resources*, OntoLex 2008 (WOLF).
- J.-P. Prost, *HOLINET 1.0*, ORTOLANG, 2022 (<https://hdl.handle.net/11403/holinet-1-0/v1>).

## Installation

```
pip install -r requirements.txt
jupyter notebook notebooks/
```
Ordre de lecture conseillé : `01` → `02` → `03` (cœur du projet) ; `04` est une piste parallèle. Les notebooks se lancent depuis le dossier `notebooks/` (chemins relatifs).

## Données et modèles (non inclus, trop volumineux)

À télécharger et placer à la racine du projet :

- **CamemBERT** `camembert-base-wikipedia-4gb` (fairseq)
- **HOLINET 1.0** (Prost, LPL / AMU, CC BY 4.0) : `holinet-1-0/`
- **WOLF 1.0b4** (WordNet libre du français) : `wolf-1.0b4.xml`
- **frWac** word2vec (`frWac_no_postag_no_phrase_700_skip_cut50.bin`) converti avec
  [convertvec](https://github.com/marekrei/convertvec) (à cloner dans `convertvec/`)

## Licence

Code sous licence MIT (voir `LICENSE`). Éléments tiers : voir `THIRD_PARTY_NOTICES.md`.
