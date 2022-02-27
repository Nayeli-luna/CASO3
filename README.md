
title: "Caso 3. Medidas de localizaciÃ³n. Media, mediana y moda"
author: "herrera luna silvia nayeli"
date: "23/02/2022"
output: 
  html_document:
  code_folding: hide
toc: true
toc_float: true
toc_depth: 6
number_sections: yes
---
  
  # Objetivo
  
  Determinar medidas estadÃ­sticas de localizaciÃ³n media, mediana, moda, mÃ¡ximos mÃ­nimos y rango de un conjunto de datos usando funciones de R.

# DescripciÃ³n

El proceso de este caso permite identificar las medidas de localizaciÃ³n de media, mediana, moda, mÃ¡ximos, mÃ­nimos, rango y el significado de las mismas para interpretar si una distribuciÃ³n de datos es simÃ©trica o asimÃ©trica.

Primero se presenta como determinar los estadÃ­sticos manualmente por medio de programaciÃ³n y luego se identifica como determinar estos mismos valores estadÃ­sticos de manera mÃ¡s sencilla por medio de funciones que existen en los paquete base de R para media y mediana y funciones de librerÃ­as instaladas para la moda.

En el proceso, los datos se visualizan por medio de la librerÃ­a ggplot previamente instalada, el grÃ¡fico que se muestra es el histograma con lineas verticales que representan la media, mediana y moda.

Finalmente se hace una interpretaciÃ³n del caso identificando la simetrÃ­a o asimetrÃ­a del mismo.

# Marco teÃ³rico

El software estadÃ­stico moderno como el lenguaje de programaciÃ³n R, permite el cÃ¡lculo de medias, medianas, desviaciones estÃ¡ndar entre otros estadÃ­sticos, asÃ­ como la construcciÃ³n y visualizaciÃ³n de grÃ¡ficas que presenten una "huella digital" de la naturaleza de la muestra.[@walpole2012].

En un conjunto de datos las medidas de posiciÃ³n estÃ¡n diseÃ±adas para ayudar al analista alguna medida cuantitativa de dÃ³nde estÃ¡ el centro de los datos en una muestra. [@walpole2012]

## La media

La media significa el promedio o la suma de todos los elementos divididos entre el total de la muestra, o lo que es lo mismo es un promedio de todos los elementos.

La media proporciona una medida de localizaciÃ³n central de los datos. Si los datos son datos de una muestra, la media se denota $\bar{x}$; si los datos son datos de una poblaciÃ³n, la media se denota con la letra griega $\mu$. [@anderson_estadistica_2008].

### FÃ³rmula de la media

En las fÃ³rmulas estadÃ­sticas se usa identificar el valor de la primera observaciÃ³n de la variable $x$ con $x_1$, el valor de la segunda observaciÃ³n de la variable $x$ con $x_2$ y asÃ­ con lo siguiente.

En general, el valor de la i-Ã©sima observaciÃ³n de la variable $x$ se denota $x_i$ hasta la posiciÃ³n final del conjunto de datos $x_n$.

La media se representa como $\bar{x}$. AquÃ­ la fÃ³rmula para le media.

$$
  \bar{x} = \sum_{i=1}^{n}\frac{x_i}{n} = \frac{x_1 + x_2+x_3+â¦x_n}{n}
$$
  
  ### Media aritmÃ©tica
  
  Se muestra el cÃ³digo para determinar la media, sumando cada elemento y dividiendo entre el nÃºmero de elementos que contiene la muestra.

Se construyen los valores de la muestra a partir de un vector llamado datos.

El contexto de los datos puede ser, edades, medidas de peso en kgs. de algÃºn producto, velocidades de andar en bicicleta u otros contexto en donde existan valores similares.

Se simulan datos de edades de personas.

{r}
datos <- c(40,60,50,45,65,70,95,90,45,60,43,56, 65, 80, 45, 70, 45, 75, 45, 54, 35, 46, 47, 50, 50, 60, 50, 50, 65, 50, 50, 22, 54, 68, 70, 46, 54, 55, 50, 55, 40, 68, 76, 56, 55, 45, 50, 43, 46, 47, 70, 24, 34, 54,43, 34, 45, 45, 45, 45)
datos


Se identifican valores de los datos en posiciones especÃ­fica $x_1, x_2, x_3, x_n$, siendo $n =$ `r length(datos)`

El sÃ­mbolo de ';' en R en una misma linea significa que se peden tomar como diferentes instrucciones para ahorrar lineas o renglones en el bloque de cÃ³digo.

Se determina el valor de $n$ o la cantidad de elementos en los datos con la funciÃ³n length().

{r}
datos[1]; datos[2]; datos[3]; datos[length(datos)]


La funciÃ³n paste() vista en otros casos, simplemente imprime en pantalla valores, posiblemente concatenados separados con la coma ','.

{r}
n <- length(datos)
paste("Cantidad de elmentos de la muestra =", n)


Ahora realizar el cÃ¡lculo de la media aritmÃ©ticamente.

La funciÃ³n sum() suma aritmÃ©ticamente todos los elementos de la muestra y round() redondea el resultado a ciertas posiciones decimales, por ejemplo round(valor, 2) redondeado a dos posiciones, siendo valor el resultado obtenido.

{r}
sum(datos) / n
paste("Una forma tradicional de sacar la media", round(sum(datos) / n, 2))


Esto serÃ­a lo mismo que sumar datos[1] + datos[2] + datos[3] + datos[4] + datos[5] + ... datos[`r n`] y luego dividir entre $n$
  
  ### Media en R
  
  En R la funciÃ³n mean() determina la media de un conjunto de datos, por ejemplo edades de doce personas adultos y adultos mayores, las pregunta son: Â¿cuÃ¡ntos datos hay en la muestra?, Â¿cuÃ¡l es la media de los datos? y Â¿que representa la media?.

La funciÃ³n round() redondea posiciones decimales.

{r}
media <- round(mean(datos),2)
paste("Usando mean(), para determinar la media de los datos =", media)


La media con valor de `r media` es un estadÃ­stico que representa el promedio de los `r n` datos de la muestra.

## La mediana

Otra medida de localizaciÃ³n importante es la mediana. El propÃ³sito de la mediana es reflejar la tendencia central de la muestra, de manera que no estÃ© influida por los valores extremos. Dado que las observaciones en una muestra son $x_1, x_2, . . . , x_n$, acomodados en orden de magnitud creciente, es decir, ordenados ascendentemente, la mediana de los datos estarÃ¡ dada por alguna de las maneras dependiendo si el nÃºmero de elementos es par o es impar:
  
  ### La fÃ³rmula de la mediana
  
  La mediana serÃ¡ representada por $\tilde{x}$
  
  $$ 
  \tilde{x} =\begin{Bmatrix}x_{(n+1)/2}\text{ Si n es impar,}
\\ \frac{1}{2}\cdot(x_{n/2}+x_{n/2+1})\text{ Si n es par,} \end{Bmatrix}
$$
  
  La fÃ³rmula significa que si el nÃºmero de elementos es impar, se toma el que estÃ¡ exactamente a la mitad de los datos ordenados y si por el contrario el nÃºmero de datos es par se toman el promedio de los dos nÃºmeros contiguos o seguidos, es decir que estÃ¡n a la mitad de todos los datos ya ordenados.

### Mediana matemÃ¡ticamente

Primero hacer un cÃ³digo para determinar si $n$ es nÃºmero par o impar o non.

El siguiente cÃ³digo en R, determina si el valor de $n$ es par o impar.

{r}
if (n %% 2 == 0) {
  n.par <- "par"
  print ("n es par")
} else {
  n.par <- "impar"
  print ("n es impar")
}


Para el caso de los datos hay que constatar y verificar si es es par o impar la variable $n$, con valor de `r n` entonces es `r n.par`, se elige la opciÃ³n adecuada de la fÃ³rmula.

Toda vez de haber verificado si el valor de $n$ es par o impar se hacer el cÃ¡lculo segÃºn la opciÃ³n de la fÃ³rmula.

Segundo, se ordenan y se muestran los datos y luego se verifica el elemento que estÃ¡ exactamente a la mitad de entre todos los datos.

La ordenaciÃ³n para este ejemplo se hace con la funciÃ³n order que genera las posiciones en que se ordena el vector datos, los datos se reescriben ordenados.

{r}
datos.ordenados <- datos[order(datos)]
datos.ordenados


Tercero, finalmente se aplica la fÃ³rmula segÃºn sea el caso par o impar.

{r}
datos.ordenados <- datos[order(datos)]
if (n.par == 'impar')  {
  mediana <- (datos.ordenados[(n+1)/2])  
} else {
  mediana <- 1/2 * (datos.ordenados[n/2] + datos.ordenados[n/2+1])  
}
mediana


Para este ejemplo de `r n` datos es sencillo para el cerebro encontrar la mediana y la media, sin embargo, R puede tratar y analizar grandes volÃºmenes de datos.

### Mediana con R

La manera mÃ¡s sencilla en R para determinar la mediana es mediante la funciÃ³n median(), la cual simplemente regresa el valor central de los datos ordenados, independientemente si el valor de $n$ es par o impar, de hecho debe intuirse que el cÃ³digo de la fÃ³rmula estÃ¡ encapsulado en la funciÃ³n median().

{r}
mediana <- median(datos)
print(mediana)


La mediana refleja el valor central de los datos. Como lo dice Lind (2015) es el punto medio de los valores una vez que se han sido ordenados de menor a mayor o de mayor a menor. [@lind_estadistica_2015].

Algunas veces, posiblemente cuando se detectan valores atÃ­picos o outliers de la muestra, es necesario pensar en utilizar un concepto llamado media recortada la cual se calcula nuevamente pero habiendo quitando cierto porcentaje de los valores mayores y menores del conjunto.

La funciÃ³n subset() filtra bajo una expresiÃ³n o condiciÃ³n un conjunto de datos que pueden ser vectores o data.frames. En este caso el resultado es un vector en R llamado datos.reducido.

{r}
datos.reducido <- subset(datos, datos >=40 & datos <=90)
datos
mean(datos.reducido)
median(datos.reducido)


Ahora los valores de media y mediana son mas cercanos.

## Moda

La moda es el valor que se presenta con mayor frecuencia. [@anderson_estadistica_2008]. Walpole, 2012) indica que la moda muestral es el valor que ocurre con mayor frecuencia en los datos y es el punto sobre el eje horizontal donde la curva de una distribuciÃ³n de datos tiene su punto mÃ¡ximo. [@walpole_probabilidad_2012].

En R existen varias alternativas para determina la moda de un conjunto de datos.

### Moda con table()

Se puede utilizar la funciÃ³n table() para encontrar las frecuencias y posteriormente ordenar tabla tal vez descendentemente y el valor del conjunto de datos de frecuencias de la primera posiciÃ³n serÃ¡ la moda. Algunas veces hay dos o tres valores que se repite en el mismo nÃºmero de ocasiones o que tienen la misma frecuencia, entonces hay que verificar si el conjunto de datos es bimodal o multimodal.

{r}
frecuencias <- table(datos)
frecuencias.ordenada <- frecuencias[order(frecuencias, decreasing = TRUE)]
frecuencias.ordenada
moda <- frecuencias.ordenada[1]
moda


### Moda con mfv(x)

Otra alternativa es utilizar la librerÃ­a o el paquete modeest; antes que nada deberÃ¡ instalar el paquete install.packages("modeest") , luego, se podrÃ¡ cargar la librerÃ­a con library(modest).

### Cargando la librerÃ­a modeest

{r message=FALSE, warning=FALSE}
library(modeest)


Para determinar la moda se utiliza la funciÃ³n mfv(x) en donde $x$ es el vector a utilizarse para encontrar la moda.

{r}
moda <- mfv(datos)
moda


Posiciones relativas de la media, la mediana y la moda

## Posiciones relativas de la media, la mediana y la moda

En cualquier distribuciÃ³n, cuando la la moda, la mediana y la media son iguales se interpreta como una distribuciÃ³n simÃ©trica; si los valores de media, moda y mediana son diferentes, por el contrario serÃ¡ asimÃ©trica si si los valores de media y mediana son diferentes[@lind_estadistica_2015].

La siguiente imagen muestra como se pueden presentar las grÃ¡ficas conforme y de acuerdo al histograma y a su curva de densidad.

![](images/medidas%20de%20ubicacion.jpg){width="400"}

### Paquete ggplot2

El paquete ggplot2 permite crear grÃ¡ficas y visualizar datos de una manera mÃ¡s elegante y amigable, es uno de los paquete mÃ¡s utilizados en R para representar y visualizar datos.

Las siguiente instrucciones utilizan el paquete ggplot() previamente instalado con install.packages("ggplot2") es una librerÃ­a.

Algunos tutoriales sobre ggplot se encuentran en los siguientes enlaces:
  
  -   <https://rpubs.com/anlope10/562981>
  
  -   <http://r-statistics.co/Complete-Ggplot2-Tutorial-Part1-With-R-Code.html>
  
  -   <https://www.datanalytics.com/libro_r/introduccion-a-ggplot2.html>
  
  -   <https://rstudio.com/wp-content/uploads/2015/04/ggplot2-spanish.pdf>
  
  -   <https://rpubs.com/MrCristianrl/496586>
  
  #### Cargar la librerÃ­a ggplot
  
  {r message=FALSE, warning=FALSE}
library(ggplot2)


### data.frame de los datos

Las siguiente lineas permiten crear un conjunto de datos data.frame a partir del vector de datos. Esto transformaciÃ³n de datos tiene la finalidad de tratar con data.frame en lugar de vector y es mÃ¡s prÃ¡ctico para efecto de visualizaciÃ³n de datos con ggplot().

{r}
df.datos <- data.frame(datos)
df.datos


### Histograma de los datos

{r}
ggplot(data = df.datos, mapping = aes(x = datos)) +
  geom_histogram(bins = 30) +
  ggtitle('Histograma de datos') +
  xlab('Valores') + ylab('Frecuencia') 



### Referencia media , mediana y moda

{r}
titulo <- "Histograma de los datos"
subtitulo <- paste("Media=",media, " Mediana = ",mediana, " Moda=",moda)
ggplot(data = df.datos, mapping = aes(x=datos)) +
  geom_histogram(bins=30) +
  ggtitle(titulo, subtitle = subtitulo) +
  xlab('Valores') + ylab('Frecuencia') +
  geom_vline(aes(xintercept = media,
                 color = "media"),
             linetype = "dashed",
             size = 1)  +
  geom_vline(aes(xintercept = mediana,
                 color = "mediana"),
             linetype = "dashed",
             size = 1) +
  geom_vline(aes(xintercept = moda,
                 color = "moda"),
             linetype = "dashed",
             size = 1) 



{r}
if (media > mediana) {
  mensaje <- "De acuerdo y conforme a la grÃ¡fica la distribuciÃ³n es asimÃ©trica con sesgo positivo dado que la media es mayor que la mediana."
} else if (media < mediana) {
  mensaje <- "De acuerdo y conforme a la grÃ¡fica la distribuciÃ³n es asimÃ©trica con sesgo negativo dado que la media es menor que la mediana."
} else if (media == mediana & mediana == moda) {
  "De acuerdo y conforme a la grÃ¡fica la distribuciÃ³n es simÃ©trica dado que la media es igual a la median y a la moda."
}



InterpretaciÃ³n: `r mensaje`

## MÃ­nimo y mÃ¡ximos

Los valores mÃ¡ximos y mÃ­nimos de un conjunto de dato son los valores de la lista de valores mÃ¡s pequeÃ±os y mas grande en la lista de los datos. Se puede observar los valores mÃ¡ximos y mÃ­nimos con los datos ordenados y verificar el primer y Ãºltimo elemento de la lista. Se utiliza el vector de datos ordenados.

{r}
datos.ordenados


Se puede determinar con las funciones max() y min() para encontrar los valores mÃ¡ximos y mÃ­nimos respectivamente.

{r}
max(datos)
min(datos)


## Rango

El rango de un conjunto de datos es el intervalo que existe entre los valores, es decir desde el valor mÃ­nimo hasta el valor mÃ¡ximo.

Con los valores de mÃ¡ximo y mÃ­nimo la diferencia que existe entre ellos determina el rango.

{r}
datos.ordenados[n] - datos.ordenados[1]
max(datos) - min(datos)


Con la funciÃ³n range() en R, se obtiene los valores mÃ¡ximos y mÃ­nimos y con estos se obtiene el rango con la funciÃ³n diff()

{r}
range(datos)
diff(range(datos))


## Cuartiles

Los cuartiles son una herramienta que se usa en estadÃ­stica y que sirve para administrar grupos de datos previamente ordenados.

Los cuartiles son los tres valores de la variable que dividen a un conjunto de datos ordenados en cuatro partes iguales.

![](images/cuartiles.jpg){width="400"}

![](images/cuartiles%20cuatro-01.jpg){width="400"}

{r}
cuartiles <- quantile(datos, c(0.25, 0.50, 0.75))
cuartiles


Diagrama de caja

El diagrama de caja representa los cuartiles de los datos e identifica los valores considerados outliers o valores extremos.

Diagrama de caja con la funciÃ³n ggplot() que requiere librerÃ­a ggplot2

{r}
ggplot()+
  geom_boxplot(aes(x = datos))


Diagrama de caja con la funciÃ³n boxplot() que NO requiere

{r}
boxplot(datos, horizontal = TRUE)


## FunciÃ³n summary()

Existe una funciÃ³n en R llamada summary() muy utilizada que describe y presenta la mayorÃ­a de los estadÃ­sticos citados para caso; identifica los valores mÃ­nimo, mÃ¡ximo, media y mediana de un conjunto de datos.

{r}
summary(datos)


# InterpretaciÃ³n
¿Qué significa los estadísticos descriptivos media, mediana y moda de un conjunto de datos?
  Mediana: Es el valor que se encentra en el medio en un conjunto de datos. Media: Es el promedio de los datos Moda: Es el valor del dato que se repite mas

La cantidad de elementos de los datos es de `r n`, los valores mÃ¡ximos y mÃ­nimos estÃ¡n en un rango de `r diff(range(datos))` siendo los valores mÃ¡ximo y mÃ­nimos `r min(datos); max(datos)`.

La media es de `r media`, la mediana es `r mediana` y la moda es `r moda`, habiendo alguna diferencia en donde la media es mayor que la mediana la distribuciÃ³n es asÃ­ncrona con sesgo positivo.
