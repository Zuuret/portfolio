# Optimiser des applications – Compression de modèles par Knowledge Distillation

## L’objectif principal de mon stage

L’objectif principal de mon stage était d’étudier des techniques de compression de modèles, en particulier à travers la **knowledge distillation**.

---

## Ciblage des modèles : de la base à l’optimisation

La première étape consistait à identifier une tâche sur laquelle un **Large Language Model (LLM)** comme *CodeBERT* atteignait au moins **80 % de précision**, sans modification du modèle, uniquement grâce à un traitement rigoureux des données. 

Une fois cette base établie, il fallait identifier un **Small Language Model (SLM)**, comme *TinyBERT*, qui devait initialement atteindre environ **60 % de précision** sur la même tâche, afin de créer une **marge d’amélioration justifiant la distillation**.

Un des premiers défis rencontrés concernait les jeux de données. Certains présentaient de très bonnes performances sur les deux modèles, rendant la distillation peu pertinente (le SLM ne pouvant pas « rattraper » le LLM). J’ai donc dû chercher, tester et analyser de nouveaux jeux de données, d’abord à partir de critères théoriques (**taille**, **qualité des labels**, **équilibre des classes**), puis par des expérimentations concrètes (**fine-tuning**, **évaluation des performances**, **visualisation des distributions**).

---

## Fine-tuning des modèles

Une fois les modèles choisis (*CodeBERT* atteignant **90 %** et *TinyBERT* environ **72 %** après fine-tuning), j’ai spécialisé ces deux modèles sur une tâche bien précise : **la détection de vulnérabilités dans les Smart Contracts**.

J’ai mis en œuvre différentes techniques de **fine-tuning** et j’ai réalisé un suivi hebdomadaire sous forme de **présentations synthétiques** pour mon tuteur de stage. Ces échanges m’ont permis de mieux définir les prochaines étapes et d’approfondir certaines pistes techniques.

---

## Compression via knowledge distillation

L’étape suivante était le cœur du sujet : **l’optimisation du modèle par distillation**. Encadré par mon maître de stage, j’ai commencé à m’auto-former à cette technique avancée.

La **knowledge distillation** consiste à entraîner un modèle compact (*student*) à imiter le comportement d’un modèle plus puissant (*teacher*), en espérant ainsi reproduire des performances proches tout en réduisant la **complexité du modèle**.

J’ai mis en œuvre une distillation de type **response-based**, où le modèle *student* apprend à reproduire les sorties (*logits*) du modèle *teacher*. J’ai également conçu un **script d’expérimentation** permettant de tester différentes combinaisons de paramètres :

- **Alpha** : régule la pondération entre la vraie vérité terrain et les prédictions du *teacher*.
- **Température** : adoucit les sorties du *teacher* pour faciliter l’apprentissage du *student*.

---

## Ouverture vers des techniques avancées

Au-delà de la distillation classique, je me suis également documenté et ai commencé à explorer d’autres approches d’optimisation :

- **Initialisation partielle** du *student* à partir de certaines couches du *teacher*.
- **Allègement de l’architecture** (réduction du nombre de couches, suppression du pooler).
- Concepts avancés :
  - *Mixtures of Experts*
  - *Structure bottleneck*
  - *Distillation multi-niveaux* (logits, attention, représentation intermédiaire)

Même si je n’ai pas pu implémenter toutes ces méthodes par manque de temps, ce travail m’a permis de :

- Développer une **vision approfondie de l’optimisation** de modèles de langage.
- Mieux comprendre les **enjeux liés aux compromis entre performance et légèreté**.
- Acquérir des **compétences concrètes en expérimentation, évaluation et ingénierie de modèles IA**.
