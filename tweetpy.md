# Extracción de tweets pasados con Python

Primero, instalamos las librerías con las que vamos a trabajar.

```
pip install tweepy
pip install csv
pip install pandas
```
Después, como hacemos en R, importamos/ejecutamos dichas librerías:

```
import tweepy
import csv
import pandas as pd
```

Una vez importadas, indicamos nuestras claves para conectarmos a la API de Twitter. Recordad que las obtenemos en el servicio de apps de Twitter, en esta url https://apps.twitter.com/. Debéis sustituir estas claves por las vuestras:

```
consumer_key = 'kX3iBW5z4QAJb93wzQix5j1rD'
consumer_secret = '9wn1t2aIG0MSmXhNkBF8pbjR9ll1zmJJ6xZqzaVa83H0f2Dvsw'
access_token = '429399439-zzGXG5XfwkymwQdstBr1F5CudAWlgIN4unYKTW2q'
access_token_secret = 'VUgDORB8IlL7Pq9ZBWTnISF4EcAdcs5t5aOwi347E9IqT'
```

```
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth,wait_on_rate_limit=True)
```

Creamos una variable en la que almacenamos los datos generados:

```
csvFile = open('tweets.csv', 'a')
```

Una vez almacenados esos datos, creamos una nueva variable para grabarlos en un archivo csv:

```
csvWriter = csv.writer(csvFile)
```

Por úlimo, escribimos un loop para recorrer Twitter con el hastaga que indiquemos. Esta parte del código es la que realmente extrae los tuits. ¡Atención! Puede resultar confuso ya que antes hemos declarado diferentes variables que de no llegar a este punto estarían vacías.

```
for tweet in tweepy.Cursor(api.search,q="#OTFinal",count=1000,
                           lang="es",
                           since="2018-02-01").items():
    print (tweet.created_at, tweet.text)
    csvWriter.writerow([tweet.created_at, tweet.text.encode('utf-8')])

```

La documentación de la librería tweetpy con la que podéis diseñar y definir las búsquedas podéis encontarla en este enlace: http://tweepy.readthedocs.io/en/v3.5.0/

Algunos conceptos que hemos incluidos en el loop/bucle anterior:
* q: define la búsqueda que queremos realizar.
* count: número de tuits por conexión a extraer.
* lang: idioma en el que se buscarán los tuits.
* since: define la fecha a partir de la que comenzará la búsqueda.

Una vez tengamos el cógido listo, lo guardamos con nombre twitter.py. Lo importante es que nuestro archivo tenga el formato .py.

Vamos a la consola donde ejecutaremos el código. Primero nos movemos hasta la carpeta en que queremos guardar nuestro archivo (recordad los comandos c: cd https://www.digitalcitizen.life/command-prompt-how-use-basic-commands ) y escribimos:

```
python twitter.py
```

En caso de que tengamos algún límite en la búsqueda de tuits, podemos cambiar la configuración de nuestra cuenta aquí: https://developer.twitter.com/en/docs/tweets/search/api-reference/get-search-tweets.html

Código completo:

```
import tweepy
import csv
import pandas as pd

consumer_key = 'kX3iBW5z4QAJb93wzQix5j1rD'
consumer_secret = '9wn1t2aIG0MSmXhNkBF8pbjR9ll1zmJJ6xZqzaVa83H0f2Dvsw'
access_token = '429399439-zzGXG5XfwkymwQdstBr1F5CudAWlgIN4unYKTW2q'
access_token_secret = 'VUgDORB8IlL7Pq9ZBWTnISF4EcAdcs5t5aOwi347E9IqT'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth,wait_on_rate_limit=True)

csvFile = open('tweets.csv', 'a')

csvWriter = csv.writer(csvFile)

for tweet in tweepy.Cursor(api.search,q="#OTFinal",count=1000,
                           lang="es",
                           since="2018-02-01").items():
    print (tweet.created_at, tweet.text)
    csvWriter.writerow([tweet.created_at, tweet.text.encode('utf-8')])

```


