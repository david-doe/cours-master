---
cours: Scoring
code_ue:
semestre: S1
statut: À réviser
date_examen: 2026-12-15
type_evaluation: Examen terminal et Projet
tags:
  - cours
---

# Scoring

# Cours complet : Data Science, Ingénierie du Scoring et Évaluation des Modèles

## Chapitre 1 : Fondements conceptuels et mathématiques de l'évaluation

### 1. La trilogie fondamentale : Agrégat, Inertie et Métrique

- **Agrégat :** mesure synthétique calculée à partir d'un ensemble d'observations. L'exemple de référence est la **moyenne**.
    
      
    
- **Inertie :** agrégat qui attribue une valeur mathématique globale à une distribution ou à un ensemble, mais qui, pris isolément sans combinaison, ne possède **aucune signification propre** et ne peut être interprété directement.
    
      
    - _Exemples :_ la **variance** ou la **somme des carrés expliquée (SCE)**. Une valeur de variance brute ne permet pas à elle seule de porter un jugement qualitatif sur un phénomène sans repère extérieur.
        
          
        
- **Métrique de qualité :** combinaison d'agrégats ou d'inerties dont le résultat produit un indicateur normé et interprétable.
    
      
    - _Rôle :_ servir de référence pour **jauger, mesurer et évaluer** un aspect précis d'un modèle afin de déterminer objectivement s'il est performant ou non.
        
          
        

### 2. Décomposition de l'inertie et construction d'une métrique : du SCE au $R^2$

La variabilité totale d'un modèle se décompose en inerties complémentaires :

  

- **SCE :** Somme des Carrés Expliquée (variabilité captée par le modèle).
    
      
    
- **SCR :** Somme des Carrés des Résidus (variabilité non expliquée / erreurs).
    
      
    
- **SCT :** Somme des Carrés Totaux (variabilité totale observée).
    
      
    

Prises seules, la SCE et la SCT ne permettent pas d'évaluer la qualité de l'ajustement. En combinant ces deux inerties au sein d'un quotient rationnel, on obtient le **coefficient de détermination ($R^2$)**, qui constitue une métrique d'évaluation :

  

$$R^2 = \frac{\text{SCE}}{\text{SCT}}$$

  

- **Cas particulier d'équivalence :** le coefficient de détermination ($R^2$) est égal au carré du coefficient de corrélation linéaire uniquement dans le cadre d'une **régression linéaire simple** (un modèle ne comportant qu'une seule variable explicative).
    
      
    
- **Interprétation rigoureuse :** une valeur de $R^2 = 0,8$ signifie littéralement que **80 % de la variance (ou des variations) de la variable dépendante ($Y$) sont expliqués par les variations des variables explicatives ($X$) du modèle**.
    
      
    

## Chapitre 2 : Théorie et ingénierie du scoring

### 1. Définition de l'ingénierie du scoring

L'ingénierie du scoring est l'intersection de trois dimensions :

  

- **L'approche métier (orientée « objet ») :** définit la finalité opérationnelle et les objectifs stratégiques à atteindre via le modèle.
    
      
    
- **L'approche technique (orientée « sujet ») :** traite les données, les variables et l'architecture algorithmique nécessaires pour atteindre l'objectif.
    
      
    
- **Les contraintes :** intègrent le cadre réglementaire, opérationnel et informatique de l'organisation.
    
      
    

### 2. Distinction fondamentale : Score outil business vs Scoring Data Science

Il ne faut pas confondre la note opérationnelle d'aide à la décision et la mesure de performance scientifique :

  

- **Le score pour un outil business :** note ou classification concrète attribuée à un individu ou un dossier (ex. : note de risque de crédit de 1 à 5 calculée à partir d'une équation $Y = \beta_0 + \beta_n X_n$) adossée à un seuil décisionnel d'action fixé de façon arbitraire par la direction et le métier (ex. : rejet automatique de la demande de crédit si le score $\ge 3,8$).
    
      
    
- **Le scoring en Data Science :** processus d'évaluation scientifique de la performance du modèle statistique via des métriques objectives ($R^2$, AUC, matrices de confusion). La robustesse du score business dépend directement de la qualité du scoring Data Science en amont.
    
      
    

### 3. Les trois facteurs déterminants de la performance d'un modèle

1. **La qualité des données (facteur n° 1) :** la volumétrie (nombre d'observations) et la granularité (nombre de variables explicatives et diversité des modalités pour les variables qualitatives). Un échantillon trop réduit (ex. : 30 lignes et une variable) rend tout apprentissage statistique rigoureux impossible.
    
      
    
2. **Le choix du modèle et des métriques :** adéquation de l'algorithme au problème et pertinence des indicateurs de contrôle.
    
      
    
3. **L'entraînement et l'interprétabilité :** optimisation des méthodes de validation et capacité à expliquer le comportement du modèle.
    
      
    

### 4. Les trois domaines du scoring et flexibilité méthodologique

L'ingénierie du scoring nécessite d'articuler en permanence :

  

- **Le domaine d'application (métier)** ;
    
      
    
- **Le domaine scientifique (théorique)** ;
    
      
    
- **Le domaine technique (opérationnel)**.
    
      
    

#### Modèle descriptif (bilan) vs modèle prédictif

- **Modèle descriptif :** vise uniquement à dégager des tendances ou synthétiser une base existante ; il ne requiert pas de garanties prédictives lourdes.
    
      
    
- **Modèle prédictif :** requiert impérativement la vérification stricte des hypothèses mathématiques sous-jacentes : homoscédasticité et stabilité temporelle de l'erreur, $R^2$ élevé, significativité statistique des variables au test de Student ($p\text{-value}$).
    
      
    

#### Flexibilité opérationnelle vs rigidité théorique

Les manuels académiques imposent des seuils d'acceptation rigides (seuil $\alpha = 5\,\%$, voire $1\,\%$ pour les cadres méticuleux). Dans le monde réel, exiger un seuil de $1\,\%$ sur des flux de production opérationnels est souvent irréaliste. L'ingénieur doit comprendre le sens profond des tests pour savoir quand assouplir pragmatiquement ces règles sans fragiliser la robustesse de la décision.

  

### 5. Posture de l'ingénieur : recherche objective vs idéologie d'un modèle

- **L'idéologie d'un modèle :** biais cognitif consistant à préférer systématiquement un algorithme familier ou confortable (ex. : utiliser toujours une régression logistique par automatisme) en postulant qu'il est meilleur, sans comparaison empirique.
    
      
    
- **La recherche objective :** démarche scientifique imposant de comparer les performances réelles de plusieurs familles d'algorithmes (ex. : régression logistique vs arbre de décision) pour retenir le plus performant face à la problématique métier posée.
    
      
    

## Chapitre 3 : Taxonomie des modèles et paysage industriel

### 1. Classification structurelle des modèles

La modélisation s'organise en deux grandes familles mathématiques, divisées chacune en deux sous-classes selon le type de cible :

  

```
                        MODÈLES DE DATA SCIENCE
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
   POLYNOMIAUX                                        NON POLYNOMIAUX
 (Formulation fonctionnelle)                     (Pas de formulation analytique)
         │                                                   │
   ┌─────┴─────┐                                       ┌─────┴─────┐
   ▼           ▼                                       ▼           ▼
Classifieur  Régresseur                           Classifieur  Régresseur
(Cible qual.) (Cible quant.)                      (Cible qual.) (Cible quant.)
```

  

- **Modèles polynomiaux :** dont la relation d'entrée-sortie s'exprime sous forme d'une équation ou fonction mathématique paramétrique directe (ex. : régression linéaire, régression logistique).
    
      
    
- **Modèles non polynomiaux :** dont la logique repose sur des règles de partitionnement ou de voisinage non résumables à une simple fonction polynomiale (ex. : Random Forest, K-Nearest Neighbors).
    
      
    
- **Classifieurs :** estimation d'une variable cible qualitative (catégorielle ou binaire).
    
      
    
- **Régresseurs :** estimation d'une variable cible quantitative (continue ou numérique).
    
      
    

#### Implémentation pratique en Python

Pour les modèles non polynomiaux polyvalents (comme Random Forest), la bibliothèque exige de préciser explicitement la sous-catégorie :

  

- Variable cible qualitative : `RF.Classifier` (ou `RandomForestClassifier`)
    
      
    
- Variable cible quantitative : `RF.Regressor` (ou `RandomForestRegressor`)
    
      
    

### 2. Classement des modèles dans l'industrie

1. **Régression logistique :** modèle le plus déployé en entreprise grâce à sa simplicité de prise en main, son excellente interprétabilité et sa capacité à communiquer des coefficients compréhensibles aux décideurs métiers.
    
      
    
2. **Random Forest :** modèle ensembliste combinant plusieurs arbres de décision randomisés (via échantillonnage et sous-ensembles aléatoires de variables).
    
      
    
3. **Réseaux de neurones :** socle du Deep Learning et de l'intelligence artificielle générative.
    
      
    
4. **Support Vector Machines (SVM) :** projection vectorielle séparatrice dans des espaces géométriques de grande dimension.
    
      
    
5. **Arbre de décision (isolé) :** algorithme non polynomial rarement performant lorsqu'il est utilisé seul, car insuffisant pour battre un bon modèle polynomial sans la puissance ensembliste du Random Forest.
    
      
    

### 3. Critères de choix d'un modèle

- **Quantité de données disponibles :** la volumétrie (lignes et colonnes) dicte les choix. Un échantillon dense et propre est toujours prioritaire sur la sophistication de l'algorithme.
    
      
    
- **Complexité et nature des variables :** relations linéaires standards versus données non structurées (images médicales, texte nécessitant du Deep Learning).
    
      
    
- **Maîtrise technique et interprétabilité :** appétence de l'équipe pour assurer le débogage, le suivi en production et l'explication métier des résultats.
    
      
    

### 4. Culture scientifique : la conjecture $P = NP$

La démonstration mathématique théorique démontrant si $P = NP$ révolutionnerait l'informatique : elle signifierait que tout problème dont la solution est vérifiable en temps polynomial ($NP$) pourrait être résolu en temps polynomial ($P$), permettant de transcrire des problèmes non polynomiaux en forme polynomiale.

  

## Chapitre 4 : Méthodologie et compétences de l'ingénieur Data Scientist

### 1. La progression en Data Science : Compréhension vs Optimisation aveugle

- **L'illusion de la performance :** faire tourner en boucle des régressions ou des modèles pour observer artificiellement une hausse marginale du $R^2$ ou de l'AUC n'est pas synonyme d'apprentissage. Cette approche prépare à obtenir une note devant un jury académique, mais conduit à l'échec lors du déploiement d'une pipeline industrielle en production.
    
      
    
- **La vraie progression :** elle s'acquiert en consacrant 10 à 20 heures à disséquer la construction théorique d'une métrique (ex. : calcul manuel d'une AUC) ou d'un algorithme. Cette maîtrise conceptuelle constitue une brique définitivement capitalisée pour toute la carrière.
    
      
    

### 2. Outils et marché du travail

- **Langage de référence :** **Python 3** est impératif pour la Data Science et le Machine Learning industriel. R reste utile pour l'analyse académique mais s'avère pénalisant pour l'intégration en production.
    
      
    
- **Environnement de travail :** maîtrise de l'algorithmique sous Jupyter Lab / Jupyter Notebook.
    
      
    
- **Exigences industrielles et IA :** face à la multiplication des prompts non maîtrisés, les recruteurs multiplient les tests techniques individuels pour éliminer les profils incapables de maîtriser ce qu'ils déploient en production.
    
      
    
- **Consignes de livrable pour le projet :**
    
      
    - Comparer rigoureusement une **régression logistique** et un **arbre de décision** (pas de SVM, ni de forêt aléatoire, ni de réseau de neurones).
        
          
        
    - Restitution sous forme de document **HTML** commenté et structuré pas à pas (expliquer la démarche, ne pas se contenter de sorties de code brutes).
        
          
        

## Chapitre 5 : Métriques d'évaluation de la classification et cas pratique

### 1. Indicateurs clés de performance

- **Matrice de confusion :** croisement entre l'état réel et la prédiction ($VP$ : Vrais Positifs, $VN$ : Vrais Négatifs, $FP$ : Faux Positifs, $FN$ : Faux Négatifs).
    
      
    
- **Précision :** capacité à ne prédire que des éléments pertinents :
    
      
    
    $$\text{Précision} = \frac{VP}{VP + FP}$$
    
      
    
- **Rappel (Sensibilité ou $TPR$) :** capacité à détecter tous les événements positifs réels :
    
      
    
    $$\text{Rappel} = \frac{VP}{VP + FN}$$
    
      
    
- **$F_1$-Score :** moyenne harmonique équilibrant précision et rappel :
    
      
    
    $$F_1\text{-score} = 2 \cdot \frac{\text{Précision} \cdot \text{Rappel}}{\text{Précision} + \text{Rappel}}$$
    
      
    
- **Accuracy (Exactitude globale) :** proportion de prédictions exactes sur l'ensemble des prédictions :
    
      
    
    $$\text{Accuracy} = \frac{VP + VN}{VP + VN + FP + FN}$$
    
      
    
- **gAUC (Generalized AUC) :** évaluation pondérée de la capacité discriminante entre différentes sous-classes selon leurs poids respectifs ($W_k = \frac{N_k}{N_{\text{total}}}$) :
    
      
    
    $$gAUC = \sum_{k} W_k \cdot AUC_k$$
    
      
    
    _Règle d'interprétation :_ si le $gAUC$ est excessivement proche de l'$AUC$ d'une classe donnée, cela signale que cette classe est potentiellement sous-représentée dans l'échantillon.
    
      
    
- **Coefficient de Gini :** mesure de dispersion et de différenciation dérivée de l'AUC :
    
      
    
    $$\text{Gini} = 2 \cdot AUC - 1$$
    
      
    
    _Valeurs :_ $1$ (discrimination parfaite), $0$ (modèle aléatoire), $-1$ (discrimination inversée).
    
      
    
- **MCC (Matthews Correlation Coefficient) :** coefficient mesurant la qualité globale en tenant compte symétriquement des 4 cadrans de la matrice de confusion : _Valeurs :_ $+1$ (prédiction parfaite), $0$ (aléatoire), $-1$ (désaccord total).
    
      
    
- **Test de Wald :** test d'hypothèse statistique vérifiant la significativité des paramètres estimés d'une régression logistique ($H_0 : \beta_j = 0$).
    
      
    

### 2. Tableau de synthèse des cibles attendues

|**Métrique PDF**|**Formule clé PDF+ 2**|**Cible visée PDF+ 1**|**Interprétation PDF+ 3**|
|---|---|---|---|
|**AUC**|$\sum \text{Aires des trapèzes ROC}$|**$\ge 0,8$ (viser $0,9$)**|Qualité de discrimination globale|
|**$F_1$-Score**|$2 \cdot \frac{\text{Précision} \cdot \text{Rappel}}{\text{Précision} + \text{Rappel}}$|**$0,8$**|Équilibre entre précision et rappel|
|**gAUC**|$\sum W_k \cdot AUC_k$|**$0,85$**|Équilibre inter-classes pondéré|
|**Accuracy**|$\frac{VP + VN}{\text{Total}}$|**$0,9$**|Exactitude globale des classifications|
|**Gini**|$2 \cdot AUC - 1$|Proche de **$1$**|Différenciation par rapport au hasard|
|**MCC**|Matrice de confusion globale|Proche de **$1$**|Corrélation prédiction / réalité|
|**Test de Wald**|Statistique de rapport de variance|**$p\text{-value} < 0,05$**|Significativité des coefficients estimés|

### 3. Travaux Dirigés : Calcul manuel pas à pas de la courbe ROC et de l'AUC

L'exercice porte sur un échantillon de 9 observations de test.

  

#### Étape 1 : Données brutes et tri décroissant

On ordonne l'échantillon par ordre décroissant de probabilité estimée :

  

- Total Vrais Événements ($TE$ ou $Y=1$) : **4**
    
      
    
      
    
- Total Faux Événements ($FE$ ou $Y=0$) : **5**
    
      
    
      
    

|**Observation PDF+ 1**|**Probabilité estimée PDF+ 1**|**Observé réel PDF+ 1**|**Catégorie PDF+ 1**|
|---|---|---|---|
|1|0,9|1|TE|
|2|0,8|0|FE|
|3|0,7|1|TE|
|4|0,7|0|FE|
|5|0,4|0|FE|
|6|0,4|1|TE|
|7|0,3|1|TE|
|8|0,3|0|FE|
|9|0,2|0|FE|

#### Étape 2 : Tableau cumulatif par palier distinct

On cumule les événements prédits positifs au fur et à mesure que le seuil de décision descend :

  

|**Palier (Seuil) PDF**|**Observations concernées PDF+ 1**|**Cumul TE (VP) PDF**|**Cumul FE (FP) PDF**|
|---|---|---|---|
|**Origine**|-|0|0|
|**0,9**|Obs 1|1|0|
|**0,8**|Obs 2|1|1|
|**0,7**|Obs 3 et 4|2|2|
|**0,4**|Obs 5 et 6|3|3|
|**0,3**|Obs 7 et 8|4|4|
|**0,2**|Obs 9|4|5|

#### Étape 3 : Calcul des taux d'erreur et coordonnées ROC

Formules utilisées pour chaque point :

  

- **Taux de Faux Événements ($FER$ / $FPR$ en abscisse) :**
    
      
    
    $$FER = \frac{\text{Cumul } FE}{\Sigma FE} = \frac{\text{Cumul } FE}{5}$$
    
      
    
- **Taux de Vrais Événements ($TER$ / $TPR$ en ordonnée) :**
    
      
    
    $$TER = \frac{\text{Cumul } TE}{\Sigma TE} = \frac{\text{Cumul } TE}{4}$$
    
      
    

Coordonnées des points de la courbe ROC $(FER ; TER)$ :

  

1. **Origine :** $(0 ; 0)$
    
      
    
      
    
2. **Seuil 0,9 :** $FER = \frac{0}{5} = 0 \quad ; \quad TER = \frac{1}{4} = 0,25 \implies \mathbf{(0 \,;\, 0,25)}$
    
      
    
      
    
3. **Seuil 0,8 :** $FER = \frac{1}{5} = 0,2 \quad ; \quad TER = \frac{1}{4} = 0,25 \implies \mathbf{(0,2 \,;\, 0,25)}$
    
      
    
      
    
4. **Seuil 0,7 :** $FER = \frac{2}{5} = 0,4 \quad ; \quad TER = \frac{2}{4} = 0,5 \implies \mathbf{(0,4 \,;\, 0,5)}$
    
      
    
      
    
5. **Seuil 0,4 :** $FER = \frac{3}{5} = 0,6 \quad ; \quad TER = \frac{3}{4} = 0,75 \implies \mathbf{(0,6 \,;\, 0,75)}$
    
      
    
      
    
6. **Seuil 0,3 :** $FER = \frac{4}{5} = 0,8 \quad ; \quad TER = \frac{4}{4} = 1 \implies \mathbf{(0,8 \,;\, 1)}$
    
      
    
      
    
7. **Seuil 0,2 :** $FER = \frac{5}{5} = 1 \quad ; \quad TER = \frac{4}{4} = 1 \implies \mathbf{(1 \,;\, 1)}$
    
      
    
      
    

#### Étape 4 : Calcul de l'aire sous la courbe par la méthode des trapèzes

Formule géométrique de l'aire sous deux points consécutifs :

  

$$\text{Aire}_i = \frac{(FER_{i+1} - FER_i) \cdot (TER_i + TER_{i+1})}{2}$$

  

- **$\text{Aire}_1$** (entre $(0 ; 0)$ et $(0 ; 0,25)$) :
    
      
    
    $$\text{Aire}_1 = \frac{(0 - 0) \cdot (0 + 0,25)}{2} = \mathbf{0}$$
    
      
    
- **$\text{Aire}_2$** (entre $(0 ; 0,25)$ et $(0,2 ; 0,25)$) :
    
      
    
    $$\text{Aire}_2 = \frac{(0,2 - 0) \cdot (0,25 + 0,25)}{2} = \frac{0,2 \cdot 0,5}{2} = \mathbf{0,05}$$
    
      
    
- **$\text{Aire}_3$** (entre $(0,2 ; 0,25)$ et $(0,4 ; 0,5)$) :
    
      
    
    $$\text{Aire}_3 = \frac{(0,4 - 0,2) \cdot (0,25 + 0,5)}{2} = \frac{0,2 \cdot 0,75}{2} = \mathbf{0,075}$$
    
      
    
- **$\text{Aire}_4$** (entre $(0,4 ; 0,5)$ et $(0,6 ; 0,75)$) :
    
      
    
    $$\text{Aire}_4 = \frac{(0,6 - 0,4) \cdot (0,5 + 0,75)}{2} = \frac{0,2 \cdot 1,25}{2} = \mathbf{0,125}$$
    
      
    
- **$\text{Aire}_5$** (entre $(0,6 ; 0,75)$ et $(0,8 ; 1)$) :
    
      
    
    $$\text{Aire}_5 = \frac{(0,8 - 0,6) \cdot (0,75 + 1)}{2} = \frac{0,2 \cdot 1,75}{2} = \mathbf{0,175}$$
    
      
    
- **$\text{Aire}_6$** (entre $(0,8 ; 1)$ et $(1 ; 1)$) :
    
      
    
    $$\text{Aire}_6 = \frac{(1 - 0,8) \cdot (1 + 1)}{2} = \frac{0,2 \cdot 2}{2} = \mathbf{0,2}$$
    
      
    

#### Étape 5 : Sommation et résultat final de l'AUC

$$AUC = \sum_{i=1}^{6} \text{Aire}_i = 0 + 0,05 + 0,075 + 0,125 + 0,175 + 0,2 = \mathbf{0,625}$$

  

- **Diagnostic :** avec une valeur de $0,625$, le modèle se situe nettement en dessous du seuil minimal acceptable en industrie ($0,8$) et de la cible idéale ($0,9$) ; il nécessite un réentraînement ou une révision de ses variables explicatives.

