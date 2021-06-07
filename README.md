```{r, eval=FALSE, include=TRUE}
"Protocolo:

 1. Daniel Felipe Villa Rengifo

 2. Lenguaje: R

 3. Tema: Ejercicios con la App Science Journal de Google

 4. Fuentes:
    https://play.google.com/store/apps/details?id=cc.arduino.sciencejournal&hl=es_CO&gl=US"
```
Profe este tema lo trabaje sin librerias (fue muy complicado, me costo mucho) ah espero que sea de su agrad y utlice la app que antes era de google y ahora es de arduino

# ¿Que esta pasando?

**_Lo que va a suceder a continuación es que voy a explicar el funcionamiento de la aplicación_** **_[Science Journal](https://sciencejournal.withgoogle.com/experiments/getting-started-with-motion/)._**

Los objetos tienden a permanecer en su sitio o a seguir moviéndose si se mueven; a esto le llamamos inercia de tendencia. La Primera Ley de Newton expresa esta idea formalmente: un objeto continúa en su estado de movimiento o reposo a menos que actúe sobre él una fuerza desequilibrada.

Cuando una fuerza desequilibrada hace que un objeto se mueva, decimos que el objeto acelera: su velocidad o velocidad cambia, ya sea acelerando, disminuyendo o cambiando de dirección. La aceleración se mide como un cambio de velocidad (metros por segundo) en el tiempo, o metros por segundo al cuadrado m/s^2.

Su teléfono tiene un dispositivo para medir estos cambios en movimiento: un acelerómetro. Dentro de un acelerómetro, las pequeñas masas suspendidas pueden moverse libremente. Los cambios en el movimiento hacen que estas masas se muevan, al igual que su propia cabeza tiende a caerse cuando está en un automóvil que se detiene repentinamente. Al medir estos sutiles cambios de inercia, un acelerómetro en un teléfono puede detectar cambios en el movimiento y la orientación, útil para cambiar la pantalla del modo horizontal al vertical, para jugar juegos en su teléfono y más.

![XYZ](https://sciencejournal.withgoogle.com/static/images/pages/experiments/getting-started-with-motion/phone-axis.jpg)

Probablemente notó una aceleración persistente en el eje Z, incluso con el teléfono sentado en una mesa. Esta es la aceleración que experimentamos aquí en la superficie de la Tierra debido al tirón de la gravedad, aproximadamente 9.8 m/s^2.


Vamos a tomar datos que tome con mi celular, para analizarlos y sacar sus respectivas bases de datos y graficas.

En diferentes estados:

1. Camianta Normal
2. Caminata Rapida
3. Bicleta
4. Sentado

```{r,echo = FALSE, results = 'hide'}
## Lectura de las bases generadas de la app Science Journal.
```

```{r, echo= FALSE, results= 'hide'}
Caminata_normal_Grabaci_n <- read.csv("Caminata_normal_Grabaci_n.csv")
Sentado_Grabaci_n  <-  read.csv("Sentado_Grabaci_n.csv")
Bicicleta_grabaci_n <- read.csv("Bicicleta_grabaci_n.csv")
Caminata_rapida_Grabaci_n  <-  read.csv("Caminata_rapida_Grabaci_n.csv")
```

```{r,  echo= FALSE, results= 'hide'}
#Vamos a añadir nuevas columnas a nuestras bases de datos
```

```{r, echo= FALSE, results= 'hide'}
# Para el caso de la caminata.
# Calculo de la fecha
Caminata_normal_Grabaci_n$fecha <- as.POSIXct(Caminata_normal_Grabaci_n$timestamp/1000, origin = "2019-09-27")

# Calculo del tiempo Relativo
Caminata_normal_Grabaci_n$tiempo_relativo = as.numeric(Caminata_normal_Grabaci_n$fecha - min(Caminata_normal_Grabaci_n$fecha))
```

```{r, results = 'hide'}
# Para el caso de la caminata rapida.
```

```{r, echo= FALSE, results= 'hide'}
# Calculo de la fecha
Caminata_rapida_Grabaci_n$fecha <- as.POSIXct(Caminata_rapida_Grabaci_n$timestamp/1000, origin="2019-09-27")

# Calculo del tiempo relativo
Caminata_rapida_Grabaci_n$tiempo_relativo = as.numeric(Caminata_rapida_Grabaci_n$fecha - min(Caminata_rapida_Grabaci_n$fecha))
```

```{r, results = 'hide'}
# Para el Caso de el medio de transporte (Bicicleta)
```

```{r}
# Calculo de la fecha
Bicicleta_grabaci_n$fecha <- as.POSIXct(Bicicleta_grabaci_n$timestamp/1000, origin = "2019-09-27")

# Calculo del tiempo relativo
Bicicleta_grabaci_n$tiempo_relativo = as.numeric(Bicicleta_grabaci_n$fecha - min(Bicicleta_grabaci_n$fecha))
```

```{r, results = 'hide'}
# Para el caso de estado de reposo (sentado).
```

```{r}
# Calculo de la fecha
Sentado_Grabaci_n$fecha <- as.POSIXct(Sentado_Grabaci_n$timestamp/1000, origin="2019-09-27")

# Calculo del tiempo relativo
Sentado_Grabaci_n$tiempo_relativo = as.numeric(Sentado_Grabaci_n$fecha - min(Sentado_Grabaci_n$fecha))
```

# Estado sentado.
```{r, results='hide', echo= FALSE}
#Resumen de la base de datos
summary(Sentado_Grabaci_n)

```

```{r}
# Revision de los primeros 10 datos de la base de datos
head(Sentado_Grabaci_n, 10)
```

```{r}
cat("\n \nde esta tabla podemos notar que en \"AccX\" y \"AccZ\" al principio respectivamente que el eje esta en su inverso (negativamente) y por esta razon tiene datos negativos, 
además, en \"Accy\" casi siempre tuve el celular en el inverso del eje y.")
```

# En caminata normal.

```{r, results='hide', echo= FALSE} 
#Resumen de la base de datos
summary(Caminata_normal_Grabaci_n)
```

```{r}
# Revision de los primeros 10 datos de la base de datos
head(Caminata_normal_Grabaci_n, 10)
```

```{r}
cat("podemos notar que como dije anteriormente, estamos utilizando la ecuación de la primera ley de newton para describir los ejes __x, y, z__ entonces vemos que en varios ejes tuve por movimientos invertidos a los REALES + (positivos) y por eso se muestra negativamente pero además de esto con la tabla anterior cambia significativamente en el \"AccZ\" ya que se ultiliza diferentes posciciones y movimientos para cuando estoy en estado sentado y en caminata normal.")
```


# En caminata rapido.

```{r, results = 'hide'}
# Resumen de la base de datos.
summary(Caminata_rapida_Grabaci_n)
```

```{r}
# LOs 10 primeros datos de la base de datos
head(Caminata_rapida_Grabaci_n, 10)
```

```{r}
cat("podemos notar que al caminar rapido se estabiliza, porque al tener el celular moviendose en diferentes direcciones en todos los ejes de una manera significativa, es decir , crea un rango promedio de ellos por la cantidad de movimiento.")
```


```{r, results = 'hide'}
# En el medio de transporte ((Bicicleta))
```

```{r, results = 'hide'}
# Resumen de la base de datos.
summary(Bicicleta_grabaci_n)
```

```{r, results = 'hide'}
# LOs 10 primeros datos de la base de datos
head(Bicicleta_grabaci_n, 10)
```
```{r}
# Con with hacemos graficos de tipo lineal
```


```{r include=FALSE}
# Sentado
png(filename = "TiempoRsentado.png", height = 720, width = 720)

with(Sentado_Grabaci_n, plot(tiempo_relativo, AccX, type = "l", main = "Tiempo relativo (seg) Sentado frente al EjeX del Telefono"))

dev.off()
```

```{r include=FALSE}
png(filename = "TiempoRCaminataN.png", height = 720, width = 720)

with(Caminata_normal_Grabaci_n, plot(tiempo_relativo, AccX, type = "l", main = "Tiempo Relativo (seg) Caminata Normal frente al Eje X del telefono"))

dev.off()
```

```{r include=FALSE}
png(filename = "TiempoRCaminataR.png")

with(Caminata_rapida_Grabaci_n, plot(tiempo_relativo, AccX, type = "l", main = "Tiempo Relativo (seg) Caminata Rapido frente al Eje X del telefono"))

dev.off()
```

```{r include=FALSE}
png(filename = "TiempoRBicicleta.png")

with(Bicicleta_grabaci_n, plot(tiempo_relativo, AccX, type = "l", main = "Tiempo Relativo (seg) en Bicicleta frente al Eje X del telefono"))

dev.off()
```


```{r}
# Añadimos nuevas columnas
## Cálculo por segundo.

Caminata_normal_Grabaci_n$segundos <- trunc(Caminata_normal_Grabaci_n$tiempo_relativo)

Caminata_rapida_Grabaci_n$segundos  <- trunc(Caminata_rapida_Grabaci_n$tiempo_relativo)

Bicicleta_grabaci_n$segundos <- trunc(Bicicleta_grabaci_n$tiempo_relativo)

Sentado_Grabaci_n$segundos  <- trunc(Sentado_Grabaci_n$tiempo_relativo)
```


```{r, results = 'hide'}
## Cálculo de la acelaración por segundo. con el promedio
```

```{r}

Caminata2_normal <- aggregate(Caminata_normal_Grabaci_n[, 2:4], 
                       by = list(segundos = Caminata_normal_Grabaci_n$segundos),
                       FUN = mean, na.rm = TRUE)

print(Caminata2_normal)
```

```{r}
Caminata2_rapida <- aggregate(Caminata_rapida_Grabaci_n[, 2:4], 
                       by = list(segundos = Caminata_rapida_Grabaci_n$segundos),
                       FUN = mean, na.rm = TRUE)

print(Caminata2_rapida)
```

```{r}
Bicicleta2 <- aggregate(Bicicleta_grabaci_n[, 2:4], 
                       by = list(segundos = Bicicleta_grabaci_n$segundos),
                       FUN = mean, na.rm = TRUE)
print(Bicicleta2)
```

```{r}
sentado2 <- aggregate(Sentado_Grabaci_n[, 2:4], 
                       by = list(segundos = Sentado_Grabaci_n$segundos),
                       FUN = mean, na.rm = TRUE)

print(sentado2)
```

```{r include=FALSE}
png(filename = "AccCaminataN.png")

# Graficamos en comparacion de los tres ejes en Grados
matplot(Caminata2_normal[, 1], Caminata2_normal[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg de los Ejes del Celular | Caminata Normal")
# Anadimos una leyenda al grafico para mejor comprensión
legend("bottomright",
       legend = names(Caminata2_normal)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(Caminata2_normal)),
       cex = 0.8)
dev.off()
```

```{r include=FALSE}
png(filename = "AccCaminataR.png")

# Graficamos en comparacion de los tres ejes en Grados
matplot(Caminata2_rapida[, 1], Caminata2_rapida[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg de los Ejes del Celular | Caminata Rapida")

# Anadimos una leyenda al grafico para mejor comprensión
legend("topright",
       inset = 0.05,
       legend = names(Caminata2_rapida)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(Caminata2_rapida)),
       cex = 0.8)

dev.off()
```

```{r include=FALSE}
png(filename = "AccBicicleta.png")

# Graficamos en comparacion de los tres ejes en Grados
matplot(Bicicleta2[, 1], Bicicleta2[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg de los Ejes del Celular | Bicicleta")

# Anadimos una leyenda al grafico para mejor comprensión
legend("bottomright",
       legend = names(Bicicleta2)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(Bicicleta2)),
       cex = 0.8)

dev.off()
```

```{r include=FALSE}
png(filename = "AccSentado.png")

# Graficamos en comparacion de los tres ejes en Grados
matplot(sentado2[, 1], sentado2[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg de los Ejes del Celular | Sentado")

# Anadimos una leyenda al grafico para mejor comprensión
legend("topleft",
       inset = 0.09,
       legend = names(sentado2)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(sentado2)),
       cex = 0.8)

dev.off()
```

```{r, results='hide'}
## Eliminar los extremos de los datos porque notamos los cambios bruscos, entoces para tenermejor esgtadistica los eliminamos
# Para caminata_normal.
```

```{r}
# Desde el segundo 10 y maximo 130, donde los datos tiene comportamientos "sueves"
caminata3_normal <- Caminata2_normal[Caminata2_normal$segundos >= 10 & Caminata2_normal$segundos <= 130, ]
# Graficamos el cambio

png(filename = "AccDEPCaminataN.png")

matplot(caminata3_normal[, 1], caminata3_normal[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg | Caminata Normal | Depurada")

# Anadimos una leyenda al grafico para mejor comprensión
legend("bottomleft",
       legend = names(caminata3_normal)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(caminata3_normal)),
       cex = 0.8)

dev.off()
```


```{r}
# para la caminata_rapida

# Desde el segundo 10 y maximo 130, donde los datos tiene comportamientos "sueves"
caminata3_rapida <- Caminata2_rapida[Caminata2_rapida$segundos >= 10 & Caminata2_rapida$segundos <= 130, ]

png(filename = "AccDEPCaminataR.png")

# Graficamos el cambio
matplot(caminata3_rapida[, 1], caminata3_rapida[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg | Caminata Rapida | Depurada")

# Anadimos una leyenda al grafico para mejor comprensión
legend("top",
       legend = names(caminata3_rapida)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(caminata3_rapida)),
       cex = 0.8)

dev.off()
```

```{r, results = 'hide'}
# para la bicicleta
```

```{r}
# Desde el segundo 10 y maximo 130, donde los datos tiene comportamientos "sueves"
Bicicleta3 <- Bicicleta2[Bicicleta2$segundos >= 10 & Bicicleta2$segundos <= 130, ]

png(filename = "AccDEPBicicleta.png")

# Graficamos el cambio
matplot(Bicicleta2[, 1],Bicicleta2[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg | Bicicleta | Depurada")

# Anadimos una leyenda al grafico para mejor comprensión
legend("bottomright",
       legend = names(Bicicleta3)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(Bicicleta3)),
       cex = 0.8)

dev.off()
```

```{r, results = 'hide'}
# Para la posición sentado
```

```{r}
# Desde el segundo 10 y maximo 130, donde los datos tiene comportamientos "sueves"
sentado3 <- sentado2[sentado2$segundos >= 10 & sentado2$segundos <= 130, ]

png(filename = "AccDEPSentado.png")

# Graficamos el cambio
matplot(sentado3[, 1], sentado3[, 2:4], type = "l",
        ylab = "Movimientos en Grados °",
        xlab = "Segundos",
        main = "AceleraciónxSeg | Sentado | Depurada")

# Anadimos una leyenda al grafico para mejor comprensión
legend("right",
       legend = names(sentado3)[2:4],
       col = 1:4,
       bty = "n",
       fill=seq_len(ncol(sentado3)),
       cex = 0.8)

dev.off()
```

```{r, results = 'hide'}
## Cálculo de la acelaracón total
```

```{r}
# Añadimos a las bases de datos "3" una columna de la formula de aceleración total

caminata3_normal$AccT <- with(caminata3_normal, sqrt(AccX ^ 2 + AccY ^ 2 + AccZ ^ 2))

caminata3_rapida$AccT  <- with(caminata3_rapida, sqrt(AccX ^ 2 + AccY ^ 2 + AccZ ^ 2))

Bicicleta3$AccT <- with(Bicicleta3, sqrt(AccX ^ 2 + AccY ^ 2 + AccZ ^ 2))

sentado3$AccT <- with(sentado3, sqrt(AccX ^ 2 + AccY ^ 2 + AccZ ^ 2))
```


## Gráfica de la caminata normal
```{r}
# GRAFICAMOS y exportmos la acceleracion total de camianta normal
png(filename = "AccTCaminataN.png")

with(caminata3_normal, plot(segundos, AccT, type = "l", col = "green",
                            ylab = "Aceleración Total en Grados °",
                            xlab = "Segundos",
                            main = "Aceleración Total | Caminata Normal"))

dev.off()



cat("Podemos notar que la aceleración varia pero siempre se mantiene constante en un intermedio que es la gravedad 9.8 m/s^2, sin embargo 
su acerelación baja gracias a que al aumentar el el tiempo, es decir, llegar a los dos minutos aproximadamente iba disminuyendo la velocidad hasta parar y detener la prueba en la app.")
```


## Grafica de la caminata rapida y medio de transporte (bicicleta)
```{r}
# GRAFICAMOS y exportmos la acceleracion total de camianta rapida

png(filename = "AccTCaminataR.png")

with(caminata3_rapida, plot(segundos, AccT, type = "l", col = "red",
                            ylab = "Aceleración Total en Grados °",
                            xlab = "Segundos",
                            main = "Aceleración Total | Caminata Rapida"))

dev.off()
```

```{r}
# GRAFICAMOS y exportmos la acceleracion total de bicicleta

png(filename = "AccTBicicleta.png")

with(Bicicleta3, plot(segundos, AccT, type = "l",col = "purple",
                      ylab = "Aceleración Total en Grados °",
                      xlab = "Segundos",
                      main = "Aceleración Total | Bicicleta"))

dev.off()

cat("Gracias a que la graficas de caminata rapida, bicicleta (medio de transporte) es muy parecida a la anterior y se mantiene constante con la gravedad 9.8 m/s^2")
```

```{r}
# GRAFICAMOS y exportmos la acceleracion total de bicicleta

png(filename = "AccTSentado.png")

with(sentado3, plot(segundos, AccT, type = "l", col = "yellowgreen",
                    ylab = "Aceleración Total en Grados °",
                    xlab = "Segundos",
                    main = "Aceleración Total | Sentado"))

dev.off()

cat("De esta grafica se puede notal que al estar sentado varia mucho la aceleración, todos los ejes cambiaron su dirección y por el movimiento de mi pierna al pisar consecutivamente y rapido hace que esta grafica no tenga un intervalo en el cual nos podamos basar, mas bien su rango es muy disperso.")
```
