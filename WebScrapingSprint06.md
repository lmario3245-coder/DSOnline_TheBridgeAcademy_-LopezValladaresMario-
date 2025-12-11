```python
import requests
import pandas as pd
import json
from bs4 import BeautifulSoup

```


```python
api_key → tu API Key
year → 2023
language → en-US para inglés, es-ES para español
region → US o ES
sort_by → popularity.desc para las más populares
page → 1 (para obtener las 20 primeras)base_url = "https://api.themoviedb.org/3"
endpoint = "/discover/movie"

# Incluyendo parámetros en la URL
api_key = "TU_API_KEY"
url_usa = f"{base_url}{endpoint}?api_key={api_key}&year=2023&region=US&sort_by=popularity.desc&page=1&language=en-US"

respuesta_usa = requests.get(url_usa)
datos_usa = respuesta_usa.json()
pelis_usa = datos_usa['results']  # lista de diccionarios

```


```python
with open("./data/usa_movies.json", "r", encoding="utf-8") as f:
    pelis_usa = json.load(f)

```


```python
df_movies = pd.DataFrame(pelis_usa)
df_movies.info()
df_movies.head()

```


```python
col_seleccionadas = ["id","genre_ids","original_title","title","overview","vote_average"]
df_pop_usa = df_movies[col_seleccionadas]
querystring = {
    "api_key": api_key,
    "year": 2023,
    "region": "ES",
    "sort_by": "popularity.desc",
    "language": "es-ES",
    "page": 1
}

```


```python
url_spain = base_url + endpoint
respuesta_spain = requests.get(url_spain, params=querystring)
respuesta_spain.status_code, respuesta_spain.reason

datos_spain = respuesta_spain.json()
pelis_spain = datos_spain['results']
df_movies_spain = pd.DataFrame(pelis_spain)
df_pop_spain = df_movies_spain[col_seleccionadas]
df_base_movies = pd.concat([df_pop_usa, df_pop_spain], ignore_index=True)
df_base_movies.set_index("id", inplace=True)
df_base_movies.head()

```


```python
url_mojo = "https://www.boxofficemojo.com/year/2023/?area=ES"
respuesta = requests.get(url_mojo)
soup = BeautifulSoup(respuesta.text, "html.parser")

tabla = soup.find("table", class_="a-bordered a-horizontal-stripes a-size-base a-span12 mojo-body-table mojo-table-annotated")
thead = [th.get_text(strip=True) for th in tabla.find("thead").find_all("th")]
tbody = tabla.find("tbody").find_all("tr")

filas = []
for tr in tbody:
    celdas = [td.get_text(strip=True) for td in tr.find_all("td")]
    filas.append(celdas)

df_mojo = pd.DataFrame(filas, columns=thead)
df_mojo.set_index("Rank", inplace=True)
df_mojo.head()

```


```python
df_mojo = pd.read_excel("./data/mojo_data.xlsx", index_col="Rank")
df_mojo.info()
df_mojo.head()

```


```python
df_base_movies = df_base_movies.merge(df_mojo, left_on="title", right_on="Title", how="left")
df_base_movies.head(10)
df_base_movies.info()
df_esp_ingresos = df_base_movies[(df_base_movies['region']=='ES') & (df_base_movies['Total Gross'].notna())]
df_esp_ingresos

```


```python
df_base_movies['popularity_rank'] = df_base_movies.reset_index().index + 1

df_movies_with_box = pd.merge(df_base_movies, df_mojo, left_on="title", right_on="Title", how="inner")
df_movies_with_box.head()

```
