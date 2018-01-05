---
title       : Introduction à la Regression
description : Dans ce chapitre, nous introduisons le concept de régression du point de vue de l'apprentissage automatique. Nous présenterons la méthode de régression fondamentale - la régression linéaire. Nous montrerons comment ajuster un modèle de régression linéaire et faire des prédictions à partir du modèle.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


---
## Coder une régression à une seule variable

```yaml
type: NormalExercise
key: 333006ca56
lang: r
xp: 100
skills: 1
```

Pour le premier exercice de codage, vous allez créer une formule pour définir une tâche de modélisation à une variable, puis adapter un modèle linéaire aux données. On vous donne les taux de chômage masculin et féminin aux États-Unis sur plusieurs années ([Source](http://college.cengage.com/mathematics/brase/understandable_statistics/7e/students/datasets/slr/frames/slr02.html)).

La tâche consiste à prédire le taux de chômage des femmes à partir du taux observé de chômage masculin. Le résultat est `female_unemployment`, et l'entrée est `male_unemployment`.

Le signe du coefficient variable vous indique si le résultat augmente (+) ou diminue (-) lorsque la variable augmente.

Rappelez-vous que l'interface d'appel de lm () est:

`lm(formula, data = ___)`

`@instructions`
Les données `unemployment` est dans votre espace de travail.
`@hint`
La formule a la forme suivante `outcome ~ input1 + input2 + ....`
vous devez passer deux arguments dans la fonction `lm()`: la formile et la data frame.

`@pre_exercise_code`
```{r}
male_unemployment <- c(2.9,6.7,4.9,7.9,9.8,6.9,6.1,6.2,6.0,5.1,4.7,4.4,5.8)
female_unemployment <- c(4.0, 7.4, 5.0, 7.2, 7.9, 6.1, 6.0, 5.8, 5.2, 4.2, 4.0, 4.4,5.2)
unemployment <- data.frame(male_unemployment,female_unemployment) 
```

`@sample_code`
```{r}
# unemployment est dans votre espace de travail workspace


# Définer une formule pour exprimer female_unemployment en fonction de male_unemployment
fmla <- 

# Impriler la formule


# Utiliser la formule pour ajuster le modèle: unemployment_model
unemployment_model <- 

# Imprimer le modèle

```

`@solution`
```{r}
# unemployment est dans votre espace de travail workspace
summary(unemployment)

# Définer une formule pour exprimer female_unemployment en fonction de male_unemployment
fmla <- female_unemployment ~  male_unemployment 

# Imprimer la formule
fmla

# Utiliser la formule pour ajuster le modèle: unemployment_model
unemployment_model <- lm(fmla, unemployment)

# Imprimer le modèle
unemployment_model
```

`@sct`
```{r}
badFormula_msg <- "la formule n'est pas correcte!"
BadModel_msg <- "le modèle n'est pas correcte"

test_output_contains("fmla", incorrect_msg = badFormula_msg)
test_output_contains("unemployment_model", incorrect_msg = BadModel_msg)
success_msg("Bien!")
```


---
## Prédire du modèle de chômage

```yaml
type: NormalExercise
key: 7c4fdfa350
lang: r
xp: 100
skills: 1
```
Dans cet exercice, vous utiliserez votre modèle de chômage, `unemployment_model`, pour faire des prédictions à partir des données sur le chômage et comparer les taux de chômage prévus des femmes aux taux réels de chômage des femmes observés sur les données `unemployment`. Vous utiliserez également votre modèle pour prédire sur des nouvelles valeurs de chômage `newrates` qui consiste en une seule observation, où le chômage des hommes est de 5%.

La fonction `predict()` est utilisée sur le modèle généré par `lm` ainsi:

`predict(model, newdata)`

Vous allez utilisé le package `ggplot2` pour déssiner les plots. Il est nécéssaire d'ajouter une colonne de prédiction à la data frame `unemployment`. Vous allez corréler dans le plot le `outcome` par rapport `prediction`, et les comparer à la ligne qui représente une parfaite prédiction ()
You will use the ggplot2 package to make the plots, so you will add the prediction column to the unemployment data frame. You will plotla ligne quand au `outcome` est égale à la valeur prédite.

`@instructions`

`@hint`
- la fonction `predict()` retourne les prédictions en se basant sur le modèle 
- L'argument `newdata` de `predict()` spécifie la nouvelle data frame sur laqulle sera faite la prédiction.

`@pre_exercise_code`
```{r}
male_unemployment <- c(2.9, 6.7, 4.9, 7.9, 9.8, 6.9, 6.1, 6.2, 6.0, 5.1, 4.7, 4.4, 5.8)
female_unemployment <- c(4.0, 7.4, 5.0, 7.2, 7.9, 6.1, 6.0, 5.8, 5.2, 4.2, 4.0, 4.4, 5.2)
unemployment <- data.frame(male_unemployment,female_unemployment)
fmla <- female_unemployment ~  male_unemployment 
unemployment_model <- lm(fmla, unemployment)
newrates <- data.frame('male_unemployment' = 5)
```

`@sample_code`
```{r}
# unemployment est dans votre espace de travail
summary(unemployment)

# newrates est dans votre espace de travail
newrates

# Prédire le chômage des femmes dans la data frame unemployment
unemployment$prediction <-  predict(---, ---)

# Importer le package ggplot2
library(ggplot2)

# Dessiner le plot pour comparer les prédictions des femmes au chômage par rapport à ce qui existe réellement (mettre les prédictions sur l'axe des x). 
ggplot(---, aes(x = ---, y = ---)) + 
  --- +
  geom_abline(color = "blue")

# Predir le chômage des femmes si le taux du taux de chômage des hommes est de 5%
pred <- predict(---, ---)
# imprimer le
pred
```

`@solution`
```{r}
# unemployment est dans votre espace de travail
summary(unemployment)

# newrates est dans votre espace de travail
newrates

# Prédire le chômage des femmes dans la data frame unemployment
unemployment$prediction <-  predict(unemployment_model, unemployment['male_unemployment'])

# Importer le package ggplot2
library(ggplot2)

# Dessiner le plot pour comparer les prédictions des femmes au chômage par rapport à ce qui existe réellement (mettre les prédictions sur l'axe des x). 
ggplot(unemployment, aes(x = prediction, y = female_unemployment)) + 
  geom_point() +
  geom_abline(color = "blue")

# Predir le chômage des femmes si le taux du taux de chômage des hommes est de 5%
pred <- predict(unemployment_model, newrates)
# imprimer le
pred
```

`@sct`
```{r}
#test_output_contains("unemployment$prediction", incorrect_msg = "Fausse prédiction du chômage des femmes. Il faut utiliser le modèle et les données des #chômage des hommes.")
test_output_contains("pred", incorrect_msg = "Utiliser la valeur de 5 pour le chômage des hommes.")
success_msg("Bien!")
```

---
## Régression linéaire multi-variables (1)

```yaml
type: NormalExercise
key: 845b9c9495
lang: r
xp: 100
skills: 1
```
Dans cet exercice, vous allez travaillé avec la pression du sang ([Source](http://college.cengage.com/mathematics/brase/understandable_statistics/7e/students/datasets/mlr/frames/frame.html)), et modéliser la pression du sang en fonction de la masse et de l'age.

`@instructions`
La data frame `bloodpressure`ets dans votre espace de travail.

- Définissez une formule est exprime la pression du sang `bllod_pressure` en fonction de la masse `weight` et de l'age `age`. Affecter la formule à la variable `fmla` et imprimez la.
- Utilisez `fmla`pour ajuster le modèle linéaire pour prédire `blood_pressure` à partir de `age` et `weight` du jeu de donnée `bloodpressure`. nommez le modèle à `bloodpressure_model`.
- Imprimer le modèle et utiliser `summary()`. Est ce que la pression du sang augmente ou déscend en fonction de l'age? et la masse?.

`@hint`

- La formule prend la forme: `outcome ~ input_var1 + input_var2 + ....`
- L'appel à `lm()` se fait ainsi `lm(formula, data)`.
- Le signe de du coeffcient indique si le résultat augmente (+) ou déscend (-)  si la variable étudiée augmente.

`@pre_exercise_code`
```{r}
blood_pressure <- c(132, 143, 153, 162, 154, 168, 137, 149, 159, 128, 166)
age <- c(52, 59, 67, 73, 64, 74, 54, 61, 65, 46, 72)
weight <- c(173, 184, 194, 211, 196, 220, 188, 188, 207, 167, 217)
bloodpressure <- data.frame(blood_pressure, age, weight)
```

`@sample_code`
```{r}
# bloodpressure est dans votre espace de travail
summary(bloodpressure)

# Créer la formule et imprimer
fmla <- ...
...

# Ajuster le modèle: bloodpressure_model
bloodpressure_model <- ...

# Imprimer bloodpressure_model et fait appel à summary() 
...
...
```

`@solution`
```{r}
# bloodpressure est dans votre espace de travail
summary(bloodpressure)

# Créer la formule et imprimer
fmla <- blood_pressure ~ age + weight
fmla

# Ajuster le modèle: bloodpressure_model
bloodpressure_model <- lm(fmla, bloodpressure)

# Imprimer bloodpressure_model et fait appel à summary() 
bloodpressure_model
summary(bloodpressure_model)
```

`@sct`
```{r}
test_output_contains("fmla", incorrect_msg = "Votre foumule est mal définie")
test_output_contains("bloodpressure_model",  incorrect_msg = "Le modèle est mal ajusté") 
success_msg("Bien!")
```
---
## Régression linéaire multi-variables (1)

```yaml
type: NormalExercise
key: 6d60e29e00
lang: r
xp: 100
skills: 1
```
Maintenant nous allons faire une prédiction avec le modèle `bloodpressure_model`, ajusté prélablement.
Vous allez aussi comparer les valeurs prédites avec les valeurs expérimentales avec un le package ggplot2.
Faire appel à ggplot ainsi:

`ggplot(dframe, aes(x = pred, y = outcome)) + 
     geom_point() + 
     geom_abline(color = "blue")`

`@instructions`
Le jeu de donnée `bloodpressure` et le modèle `bloodpressure_model`sont déjà dans votre espace de travail.

- Utiliser `predict()` pour prédire la pression du sang dans le jeu de donnée `bloodpressure`. Affecter les prédictions dans une nouvelle colonne `prediction`.
- Graphiquement, comaper les valeurs de la pression du sang entre les deux colonnes `prediction` et `blood_pressure`. Mettre `predictions`dan sl'axe des x. A quel point les résultats sont-ils proches de la ligne de prédiction parfaite?

`@hint`

- Quand la prediction se fait sur les données d'essais, la forme de prédiction est `predict(model)`
- Le résultat réel est dans la colonne `blood_pressure`.

`@pre_exercise_code`
```{r}
blood_pressure <- c(132, 143, 153, 162, 154, 168, 137, 149, 159, 128, 166)
age <- c(52, 59, 67, 73, 64, 74, 54, 61, 65, 46, 72)
weight <- c(173, 184, 194, 211, 196, 220, 188, 188, 207, 167, 217)
bloodpressure <- data.frame(blood_pressure, age, weight)
fmla <- blood_pressure ~ age + weight
bloodpressure_model <- lm(fmla, bloodpressure)
```

`@sample_code`
```{r}
# bloodpressure est déjà dans votre espace de travail
summary(bloodpressure)

# bloodpressure_model est déjà dans votre espace de travail
bloodpressure_model

# prédire la pression du sang en utilisant le modèle bloodpressure_model :prediction
bloodpressure$prediction <- ...

# plot le résultat
... + 
    ...+
    geom_abline(color = "blue")
```

`@solution`
```{r}
# bloodpressure est déjà dans votre espace de travail
summary(bloodpressure)

# bloodpressure_model est déjà dans votre espace de travail
bloodpressure_model

# prédire la pression du sang en utilisant le modèle bloodpressure_model :prediction
bloodpressure$prediction <- predict(bloodpressure_model, bloodpressure )

# plot le résultat
ggplot(bloodpressure, aes(x = prediction, y = blood_pressure)) + 
    geom_point() +
    geom_abline(color = "blue")
```

`@sct`
```{r}
#test_output_contains("bloodpressure",  incorrect_msg = "Le modèle est mal ajusté") 
success_msg("Bien!")
```
