Script_NMDS
================

Packages nécessaires
----------------

```{r }
#Importation des données
library(readr)
#Calcul des paramètres écologiques
library(vegan)
#Réalisation des graphiques
library(ggplot2)
```

#Importer le tableau de données

```{r}
#Tableau de données floristiques
campagnetab3 <- read_csv("campagnetab3.csv")
head(campagnetab3)
#Selectionner que les colonne avec les espèces en entête
campagnetab3=campagnetab3[, 2:310]
#Tableau de données abiotiques
campagnenmdseco3 <- read_delim("campagnenmdseco3.csv",
";", escape_double = FALSE, trim_ws = TRUE)
View(campagnenmdseco3)
```

# Tracé des graphiques
```{r }
xmpl<-metaMDS(campagnetab3)
xmplt<-metaMDS(campagnetab3, transform='linear')
stressplot(xmpl) # graphique de shapared
stressplot(xmplt) # graphique de shapared
plot(xmpl)
```

```{r}
ordi <- ordiplot(xmpl, display="sites") # afficher les sites
campagnenmdseco3$xnmds <- ordi$sites[,1] # on récupère la 1ère coordonnée de la NMDS
campagnenmdseco3$ynmds <- ordi$sites[,2] # on récupère la 1ère coordonnée de la NMDS
```

```{r}
nmds <-
  ggplot(data=campagnenmdseco3 , aes(x=xnmds, y=ynmds, color=statucate)) +
  geom_point(aes(colour=statucate, fill=statucate), size=3, colour="black", shape=21) +
  scale_fill_manual("Satut du site", values = c("#b23630", "#4cb230", "#FFFF00" ), labels= c("Site hyper-endémmique","Site hypo-endémique" , "Site témoin" )) +
  scale_colour_manual("Satut du site", values = c("#b23630", "#4cb230" , "#FFFF00"), labels= c("Site hyper-endémmique","Site hypo-endémique", "Site témoin")) +
  scale_x_continuous("NMDS1") +
  scale_y_continuous("NMDS2") +
  guides(colour=FALSE) +
  guides(fill=FALSE) +
  theme(panel.grid.major = element_line(linetype='blank'),
        panel.grid.minor = element_line(linetype='blank'),
        panel.border = element_rect(fill=NA, color="black", size = 0.25),
        panel.background = element_rect(fill="white"),
        axis.ticks = element_line(color="black", size = 0.25),
        axis.ticks.length = unit(-0.1, "cm"),
        legend.key = element_rect(linetype='blank', fill = "white"),
        legend.key.size=unit(0.275, "cm"), legend.direction="vertical",
        legend.justification=c(1,0), legend.position=c(1,0)) +
  guides(fill = guide_legend(override.aes=list(size=2.5,linetype=0),fill = NULL, ncol=1))
nmds
