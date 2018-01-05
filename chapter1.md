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
test_output_contains("unemployment$prediction", incorrect_msg = "Fausse prédiction du chômage des femmes. Il faut utiliser le modèle et les données des chômage des hommes.")
test_output_contains("pred", incorrect_msg = "Utiliser la valeur de 5 pour le chômage des hommes.")
success_msg("Bien!")
```
