# Forense
# Gráficas de la practica de forense UIS 19-Nov-2017
# Nov 19, 2017
# Alejandra Ruiz-Jiménez, Fernanda Villalba, Andrés Casadiego.

#Set de datos

setwd("E:/Ento/Lab")
rm(list = ls())

#Datos
Data <- read.csv("Larvas_Forense_tolis.csv", header = T, sep=",", row.names= )


##install.packages("ggplot2")
library("ggplot2")


# Grafica del tamaño de las larvas vs Días

larvae <- ggplot(Data, aes(Data$dia, Data$tamanocm, shape=Data$larvae, group=Data$top)) +
  geom_point(size=2, aes(color=Data$top)) +
  geom_smooth(aes(color=Data$top), se= F, method = "loess", linetype = "dashed", size= 0.7) +
  ggtitle("Tamaño de larvas vs Días") + 
  xlab("Días") + 
  ylab("Tamaño en cm") + 
  labs(shape = "Familias", color= "Max-Min") + 
  theme(panel.background = element_rect(fill = '#F4F4F4')) 

##ggsave(larvae, filename = "Graf1_Larvas.jpg")
  

# Adultos Órdenes vs días
Data2 <- read.csv("Adultos_forense.csv", header = T, sep=",")

Adultos <- ggplot(Data2, aes(Data2$día, Data2$orden)) +
  geom_point(aes(colour = cut(Data2$cantidad,c(0, 1, 2, 3, 4, 5, 13))),  size = 3) +
  theme(panel.background = element_rect(fill = '#F4F4F4')) +
  ggtitle("Órdenes vs días") + 
  xlab("Días") + 
  ylab("Órdenes") + 
  labs(color= "Número de individuos")
  
##ggsave(Adultos, filename = "Adulto.jpg")  


# Adultos del orden Diptera
Diptera <- Data2[Data2$orden=="Diptera",]

Diptera2 <- ggplot(Diptera, aes(Diptera$día, Diptera$familia, group=Diptera$cantidad)) + geom_point(aes(color=Diptera$cantidad), size=3) + 
  theme(panel.background = element_rect(fill = '#F4F4F4')) +  
  scale_colour_gradientn(colours = terrain.colors(4)) + 
  scale_x_continuous(breaks = seq(0,19,2)) + 
  ggtitle("Familias del orden Diptera vs días") + 
  xlab("Días") + 
  ylab("Familias") + 
  labs(color= "Número de individuos")

##ggsave(Diptera2, filename = "Graf2_Diptera.jpg")




#### Intento de rango #### 
#Adultos
#scale_color_manual(name = "Cantidad",
#                     values = c("(0,1]" = "orange",
#                                "(1,2]" = "green",
#                                "(2,3]" = "blue",
#                                "(5, 13]" = "black",
#                                "(3,4]" = "yellow",
#                                "(4,5]" = "brown"),  
#                     labels = c("1", "2", "3", "4", "5", "13"))

