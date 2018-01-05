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
## Examiner un modèle

```yaml
type: NormalExercise
key: 450b6107b5
lang: r
xp: 100
skills: 1
```
Voyons le modèle que vous avez construit `unemployment`. Il y a plusieurs façons d'examiner un modèle. Chaque façon rapporte des informations différentes.
Nous allons utilisé `summary()`, `broom::glance()`, and `sigr::wrapFTest()`.

`@instructions`
L'objet `unemployment_model` est dans votre espace de travail
- Imprimer `unemployment_model`une autre fois. quelle information reporte t-il?
- Utiliser la fonction  `summary()` à `unemployment_model`. En plus des coefficients, vous avez l'erreur standard des coefficients estimés, et  la qualité de l'ajustement métriques comme R-squared.
- Utiliser la fonction `glance()`  au modèle pour voir la performance métrique de la data frame ordonnée. Pourriez-vous comparer les informations de `summary()` avec les colonnes de `glance()`?
- Utiliser `wrapFTest()`sur le modèle pour voir R-squared.


`@hint`
Toutes les functions prennent en argument l'object du modèle linéaire comme input.

`@pre_exercise_code`
```{r}
library(broom)
library(sigr)
male_unemployment <- c(2.9,6.7,4.9,7.9,9.8,6.9,6.1,6.2,6.0,5.1,4.7,4.4,5.8)
female_unemployment <- c(4.0, 7.4, 5.0, 7.2, 7.9, 6.1, 6.0, 5.8, 5.2, 4.2, 4.0, 4.4,5.2)
unemployment <- data.frame(male_unemployment,female_unemployment) 
fmla <- female_unemployment ~  male_unemployment 
unemployment_model <- lm(fmla, unemployment)
```

`@sample_code`
```{r}
# broom et sigr sont déjà chargés dans votre espace de travail
# Imprimer unemployment_model


# Utiliser summary() sur unemployment_model pour avoir les détails du modèle


# Utiliser glance() sur unemployment_model pour voir autrement les détails du modèle


# Utiliser wrapFTest() sur unemployment_model tpour voir d'autres détails importantes

```

`@solution`
```{r}
# broom et sigr sont déjà chargés dans votre espace de travail
# Imprimer unemployment_model
unemployment_model

# Utiliser summary() sur unemployment_model pour avoir les détails du modèle
summary(unemployment_model)

# Utiliser glance() sur unemployment_model pour voir autrement les détails du modèle
glance(unemployment_model)

# Utiliser wrapFTest() sur unemployment_model tpour voir d'autres détails importantes
wrapFTest(unemployment_model)
```

`@sct`
```{r}
success_msg("Bien!")
```
