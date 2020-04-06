---
title: "Script_Boxplots"
author: "Evans, E."
date: "03/08/2018"
output: word_document
---


## Document pour la réalisation d'un Boxplot

# Charger les packages nécessaires
# Importation des données (A)

```{r}
library(readr)
```

# Calcculer les indices de Similarité (B)

```{r}
library(ggpubr)
```

# Importer le tableau de donnée principal (A)
```{r}
dtfindicediv <- read_delim("dtfindicediv.csv", ";", escape_double = FALSE, trim_ws = TRUE)

head(dtfindicediv, 3)
```



# Réalisation de quelques Boxplots

```{r}
#Richesse spécifique
names(dtfindicediv)
p <-ggboxplot(dtfindicediv, x = "Statut", y = "Richesse",
              color = "Statut", palette = c("#00AFBB", "#E7B800", "#FC4E07"),
              order = c("Tem", "Faib", "End"),
              ylab = "Richesse spécifique", xlab = "Statut")

p + border(color = "black", size = 0.8, linetype = NULL)
```

# Indice de diversité de Shannon
```{r}
p <-ggboxplot(dtfindicediv, x = "Statut", y = "Shannon",
              color = "Statut", palette = c("#00AFBB", "#E7B800", "#FC4E07"),
              order = c("Tem", "Faib", "End"),
              ylab = "Indice de Shannon", xlab = "Statut")

p + border(color = "black", size = 0.8, linetype = NULL)
```


#  Indice de diversité de Simpson
```{r}
p <-ggboxplot(dtfindicediv, x = "Statut", y = "Simpson",
              color = "Statut", palette = c("#00AFBB", "#E7B800", "#FC4E07"),
              order = c("Tem", "Faib", "End"),
              ylab = "Indice de Simpson", xlab = "Statut")

p + border(color = "black", size = 0.8, linetype = NULL)
```



#  Indice de diversité de Pielou
```{r}
p <-ggboxplot(dtfindicediv, x = "Statut", y = "Pielou",
              color = "Statut", palette = c("#00AFBB", "#E7B800", "#FC4E07"),
              order = c("Tem", "Faib", "End"),
              ylab = "Indice de Pielou", xlab = "Statut")

p + border(color = "black", size = 0.8, linetype = NULL)
```
