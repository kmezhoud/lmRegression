---
title       : Introduction à la Regression
description : Dans ce chapitre, nous introduisons le concept de régression du point de vue de l'apprentissage automatique. Nous présenterons la méthode de régression fondamentale - la régression linéaire. Nous montrerons comment ajuster un modèle de régression linéaire et faire des prédictions à partir du modèle.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


---
## Exercice 1

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

`@pre_exercise_code`
```{r}
male_unemployment <- c(2.9,6.7,4.9,7.9,9.8,6.9,6.1,6.2,6.0,5.1,4.7,4.4,5.8)
female_unemployment <- c(4.0, 7.4, 5.0, 7.2, 7.9, 6.1, 6.0, 5.8, 5.2, 4.2, 4.0, 4.4,5.2)
unemployment <- data.frame(male_unemployment,female_unemployment) 
```

`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}

```
