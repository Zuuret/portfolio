<h1 class="code-line" data-line-start=0 data-line-end=1 ><a id="Travail_sur_les_donnes_pendant_mon_stage_0"></a>Travail sur les données pendant mon stage</h1>
<p class="has-line-data" data-line-start="2" data-line-end="4">Lors de mon stage, les données ont eu une importance capitale, j’ai donc dû leur accorder une attention toute particulière.<br>
En effet, pour mener à bien les tâches qui m’étaient confiées et assurer la réussite de l’objectif principal du stage — la compression de modèle — j’ai d’abord défini un sujet de recherche avec mon tuteur, puis appliqué diverses compétences pour manipuler des données, plus précisément des données textuelles.</p>
<h2 class="code-line" data-line-start=5 data-line-end=6 ><a id="Collecte_des_donnes_5"></a>Collecte des données</h2>
<p class="has-line-data" data-line-start="7" data-line-end="9">Tout d’abord, j’ai recherché des jeux de données adaptés à mes tâches sur la plateforme Kaggle.<br>
Mes critères de sélection étaient les suivants :</p>
<ul>
<li class="has-line-data" data-line-start="10" data-line-end="11">Correspondance avec la tâche à réaliser</li>
<li class="has-line-data" data-line-start="11" data-line-end="12">Bonne notation et fiabilité des jeux de données</li>
<li class="has-line-data" data-line-start="12" data-line-end="14">Taille suffisante pour un apprentissage pertinent</li>
</ul>
<p class="has-line-data" data-line-start="14" data-line-end="16">Une fois cette sélection faite, j’ai évalué chaque dataset en utilisant un Large Language Model (LLM), en l’occurrence <strong>CodeBERT</strong>, pour vérifier son efficacité sur ces données.<br>
Plus précisément, j’ai identifié une colonne pertinente dans chaque jeu de données et demandé à CodeBERT de prédire le type d’entrée correspondant.</p>
<p class="has-line-data" data-line-start="17" data-line-end="19">Cette étape s’est révélée assez complexe car, pour pouvoir passer à la phase suivante, je devais trouver un jeu de données sur lequel CodeBERT obtenait une précision supérieure à <strong>80 %</strong>.<br>
J’avais déjà une expérience préalable avec ce type de modèle, acquise lors d’un projet académique dans le cadre du cours d’analyse de données du semestre trois.</p>
<p class="has-line-data" data-line-start="20" data-line-end="22">Je connaissais notamment la manière de formater correctement les données afin de les rendre exploitables par un modèle de classification comme CodeBERT.<br>
Pour cela, j’ai développé plusieurs <strong>classes Python spécifiques</strong> à chaque dataset, permettant de standardiser et optimiser les données fournies au modèle.</p>
<h3 class="code-line" data-line-start=23 data-line-end=24 ><a id="Exemple__la_classe_VulnerabilityDataset_23"></a>Exemple : la classe <code>VulnerabilityDataset</code></h3>
<p class="has-line-data" data-line-start="25" data-line-end="26">Ces classes encapsulaient la logique de traitement propre à chaque jeu de données, notamment :</p>
<ul>
<li class="has-line-data" data-line-start="27" data-line-end="29">
<p class="has-line-data" data-line-start="27" data-line-end="28"><strong>La tokenisation des textes (extraits de code)</strong> : en utilisant un tokenizer adapté (par exemple celui de CodeBERT), le texte brut était converti en séquences numériques exploitables par le modèle. Cette étape incluait la troncation des séquences trop longues et le padding pour uniformiser leur taille conformément aux contraintes du modèle.</p>
</li>
<li class="has-line-data" data-line-start="29" data-line-end="31">
<p class="has-line-data" data-line-start="29" data-line-end="30"><strong>L’association des extraits de code à leurs labels</strong> : chaque morceau de code était relié à son étiquette correspondante, indispensable pour la classification supervisée.</p>
</li>
<li class="has-line-data" data-line-start="31" data-line-end="33">
<p class="has-line-data" data-line-start="31" data-line-end="32"><strong>La conversion en tenseurs PyTorch</strong> : les données étaient transformées en tenseurs optimisés pour les calculs GPU et compatibles avec le framework PyTorch.</p>
</li>
<li class="has-line-data" data-line-start="33" data-line-end="35">
<p class="has-line-data" data-line-start="33" data-line-end="34"><strong>La gestion des mini-lots (batches)</strong> : grâce à l’intégration avec <code>DataLoader</code>, ces classes facilitaient la création de mini-lots, permettant un entraînement plus efficace et une meilleure gestion de la mémoire.</p>
</li>
</ul>
<h2 class="code-line" data-line-start=35 data-line-end=36 ><a id="Prprocessing_et_nettoyage_des_donnes_35"></a>Préprocessing et nettoyage des données</h2>
<p class="has-line-data" data-line-start="37" data-line-end="39">Malgré ces efforts, je n’ai pas obtenu de résultats satisfaisants sur certains jeux de données à cause de leur qualité.<br>
Certains datasets présentaient un nombre insuffisant d’exemples, d’autres souffraient de données manquantes ou mal labellisées, ce qui rendait l’apprentissage contre-productif.</p>
<p class="has-line-data" data-line-start="40" data-line-end="41">Ne pouvant pas modifier directement le modèle pour l’instant, j’ai décidé de m’auto-former au <strong>prétraitement des données</strong>, une étape aussi intéressante que chronophage, car chaque dataset nécessitait un traitement spécifique.</p>
<p class="has-line-data" data-line-start="42" data-line-end="43">Pour chaque jeu de données, j’ai généré différents <strong>graphiques</strong> afin d’analyser la répartition des classes, détecter les valeurs manquantes, et décider de la meilleure stratégie :</p>
<ul>
<li class="has-line-data" data-line-start="43" data-line-end="44">supprimer les données manquantes ;</li>
<li class="has-line-data" data-line-start="44" data-line-end="46">ou, dans certains cas, appliquer du <strong>sous-échantillonnage</strong> ou du <strong>sur-échantillonnage</strong> pour rééquilibrer les classes sous-représentées.</li>
</ul>
<h2 class="code-line" data-line-start=46 data-line-end=47 ><a id="Rpartition_des_donnes_pour_lentranement_et_lvaluation_46"></a>Répartition des données pour l’entraînement et l’évaluation</h2>
<p class="has-line-data" data-line-start="48" data-line-end="50">J’ai également étudié la répartition optimale des données entre l’entraînement et l’évaluation.<br>
En effet, lors de l’entraînement d’un modèle, les données sont utilisées à deux étapes :</p>
<ul>
<li class="has-line-data" data-line-start="51" data-line-end="52"><strong>L’entraînement</strong>, où le modèle apprend à reconnaître des motifs dans les données.</li>
<li class="has-line-data" data-line-start="52" data-line-end="54"><strong>L’évaluation</strong>, où les données servent uniquement à mesurer la performance du modèle sans ajustement.</li>
</ul>
<p class="has-line-data" data-line-start="54" data-line-end="56">J’ai donc défini et ajusté cette répartition de façon empirique, par exemple en allouant <strong>70 % des données à l’entraînement</strong> sur les datasets les plus volumineux, et jusqu’à <strong>90 % pour les plus petits</strong>.<br>
Cette tâche est un compromis délicat : plus la part dédiée à l’entraînement est grande, meilleures seront les performances du modèle, mais la fiabilité de l’évaluation en pâtit.</p>
<h2 class="code-line" data-line-start=57 data-line-end=58 ><a id="Rsultats_et_acquis_57"></a>Résultats et acquis</h2>
<p class="has-line-data" data-line-start="59" data-line-end="60">Finalement, grâce à ces différentes techniques de préprocessing et à la qualité d’un <strong>nouveau jeu de données fourni par mon professeur</strong>, j’ai réussi à atteindre une précision <strong>supérieure à 80 %</strong> avec CodeBERT.</p>
<p class="has-line-data" data-line-start="61" data-line-end="62">Toutes ces étapes m’ont permis de développer une <strong>compréhension approfondie de la science des données</strong>, et plus particulièrement des enjeux liés au traitement et à la préparation des données dans le cadre de l’intelligence artificielle.</p>