# Curso_RNAseq2025
Curso RNAseq Universidad de Costa Rica

---
title: "Gráficos"
author: "Sebastian Quiros"
date: "2025-03-04"
output: html_document
---

# Graficos

## Datos
```{r}
library(ggplot2)
library(pheatmap)
library(ggrepel)

data("iris")
head(iris)
dim(iris)
```

## Dispersión
```{r}
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point(size = 3) +
  theme_minimal() +
  labs(title = "Gráfico de Dispersión de Sepal.Length vs Sepal.Width",
       x = "Longitud del Sépalo",
       y = "Ancho del Sépalo")
```

## Histograma
```{r}
ggplot(iris, aes(x = Sepal.Length, fill= Species)) + geom_histogram(binwidth = 0.3, alpha = 0.7, position = "identity") + theme_minimal() + labs(title = "Distribución de la Longitud del Sépalo",
                                                                                                                                                 x = "Longitud del Sépalo",
                                                                                                                                                 y = "Frecuencia")
```

## Boxplot
```{r}
ggplot(iris, aes(x = Species, y = Sepal.Length, fill = Species)) +
  geom_boxplot() +
  theme_minimal() +
  labs(title = "Distribución de Sepal.Length por Especie",
       x = "Especie",
       y = "Longitud del Sépalo")
```

## Barras
```{r}
ggplot(iris, aes(x = Species, fill = Species)) +
  geom_bar() +
  theme_minimal() +
  labs(title = "Cantidad de Observaciones por Especie",
       x = "Especie",
       y = "Conteo")
```

## Líneas
```{r}
ggplot(iris, aes(x = Sepal.Length, y = Petal.Length, color = Species)) +
  geom_line() +
  theme_minimal() +
  labs(title = "Relación entre Sepal.Length y Petal.Length",
       x = "Longitud del Sépalo",
       y = "Longitud del Pétalo")
```

## Densidad
```{r}
ggplot(iris, aes(x = Sepal.Length, fill = Species)) +
  geom_density(alpha = 0.5) +
  theme_minimal() +
  labs(title = "Densidad de la Longitud del Sépalo por Especie",
       x = "Longitud del Sépalo",
       y = "Densidad")
```

## Facetas
```{r}
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  facet_wrap(~ Species) +
  theme_minimal() +
  labs(title = "Gráfico de Dispersión por Especie",
       x = "Longitud del Sépalo",
       y = "Ancho del Sépalo")
```

## Violín
```{r}
ggplot(iris, aes(x = Species, y = Sepal.Length, fill = Species)) +
  geom_violin(alpha = 0.7) +
  theme_minimal() +
  labs(title = "Distribución de Sepal.Length por Especie",
       x = "Especie",
       y = "Longitud del Sépalo")
```

## Personalizado
```{r}
ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point(size = 3) +
  theme_classic() +
  labs(title = "Gráfico con Tema Clásico",
       x = "Longitud del Sépalo",
       y = "Ancho del Sépalo")
```

## Heatmap
```{r}
pheatmap(cor(iris[,1:4]), cluster_rows=TRUE, cluster_cols=TRUE, display_numbers=TRUE)
```

## Volcano
```{r}
iris$logFC <- iris$Sepal.Length - mean(iris$Sepal.Length)
iris$pvalue <- runif(nrow(iris), min=0, max=0.05)
iris$logP <- -log10(iris$pvalue)

ggplot(iris, aes(x=logFC, y=logP, color=Species, label=Species)) +
  geom_point() +
  geom_text_repel() +
  theme_minimal() +
  labs(title = "Volcano Plot de iris",
       x = "Log Fold Change",
       y = "-log10(p-value)")
```
