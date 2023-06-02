#Grafico de series tiempo
setwd("D:/DAVID/DECIMO SEMESTRE/ARTICULO TAMBO/RSTUDIO")
library(ggplot2)
library(lubridate)
library(dplyr)
library(readxl)
library(tidyverse)
datos <- read_excel("0000 Datos_pmm tambo.xlsx")
view(datos)
datos_long <- datos %>%
  pivot_longer(-Fecha, names_to = "estacion", values_to = "medida")
head(datos_long)

datos_long$Fecha <- as.Date(datos_long$Fecha)

# Crear un gráfico de línea con ggplot
ggplot(data = datos_long, aes(x = Fecha, y = medida, color = estacion)) +
  geom_line() +
  theme_minimal() +
  labs(title = "Medidas a lo largo del tiempo", x = "Fecha", y = "Precipitacion") +
  theme(legend.title = element_blank())
