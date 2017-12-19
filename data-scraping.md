Instalamos el paquete rvest. ¿Para qué sirve?
La principal función de rvest es extraer datos de la web.

```
install.packages("rvest")
```

Una vez instalado, no olvidéis cargar el paquete:

```
library(rvest)
```

Asociamos a la variable url el enlace donde se encuentra la tabala de datos que queremos extraer. En este caso un artículo de Wikiedia que incluye una tabla con el porcentaje de impuesto de sociedades que se paga en diferentes países:

```
url <- "https://en.wikipedia.org/wiki/Corporate_tax"
```

Al ser un enlace, R lo interpreta como un texto y siempre va entre comillas.

A continuación, escribimos una serie de funciones pertenecientrs al paquete rvest para:
* leer y almacenar el html
* recorrer e identificar mediante path xml dónde está la tabla que queremos extraer
* extraer la tabla del html y guardarla en R

```
is  <- url %>%
    read_html() %>%
    html_nodes(xpath='//*[@id="mw-content-text"]/div/table[5]') %>%
    html_table()
```

El resultado lo guardamos en la variable 'is' que hace renferencia a impuesto de sociedades.

Si escribimos is en la consola, comprobamos como, a pesar de haber realizado una extracción bastante limpia de los datos, todavía hay que hacer algún trabajo de limpieza. Por ejemplo, todas las columnas de la tabla extraída están en formato 'character'. Para poder visaulizarlas debemos convertirlas a número y eliminar el símbolo del %.

Para limpiar la base de datos, utilizaremos el paquete tidyverse. Primero, como siempre, lo instalamos:

```
install.packages("tidyverse")
```

Y para comenzar a utilizarlo lo cargamos en R:

```
library(tidyverse)
```

Para extraer lps datos de forma adecuada, debemos hacer unos cambios en el código anterior:

     # your xpath defines the single table, so you can use html_node() instead of html_nodes()

```
islimpio <- url %>% 
     read_html() %>% 
     html_node(xpath='//*[@id="mw-content-text"]/div/table[5]') %>% 
     html_table() %>% as_tibble() %>% 
     setNames(c("country", "corporate_tax", "combined_tax"))
```

Escribimos el nombre de la variable para comprobar que la extracción ha sido la correcta:

```
islimpio
```

Ahora es momento de convetir lls caracteres en númsros para poder visualizar qué impuesto de sociedades tiene cada uno de los países analizados. Para ello utilizaremos la función 'mutate':

```
bar <- islimpio %>% 
     mutate(corporate_tax=as.numeric(str_replace(corporate_tax, "%", "")),
            combined_tax=as.numeric(str_replace(combined_tax, "%", ""))
     )
```

Comprobamos de nuevo que hemos aplicado el código de la manera adecuada:

```
bar
```

Ahora sí, podemos visualizar los datos. Primero de todo, cargamls ggplot2:


Una vez cargada escribimos el código para dibujar un gráfico de barras.

```
visualizar <- ggplot(data=bar, aes(x=country, y=corporate_tax)) +
     geom_bar(stat="identity")
```

Comprobamos que hemos escrito el código correctamente:

```
visualizar
```
Las barras están en vertical ppr lo que no se lee bien la información del eje  x. Para rotar 90 el gráfico, aplicamos la función coord_flip():

```
p + coord_flip()
```

El resultado:

IMG
