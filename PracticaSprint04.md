```python
import pandas as pd
import numpy as np

```


```python
titulos = ["Toy Story 4", "Los Incríbles 2", "Buscando a Dory", "Toy Story 3",
           "Caco", "Inside Out", "Monsters University", "Up"]

lanzamiento = [2015, 2018, 2016, 2010, 2017, 2015, 2013, 2006]
recaudaciones = [1073, 1242, 1029, 1067, 807, 857, 744, 735]
espectadores = [74.91, 93.42, 76.72, 81.35, 62.75, 68.27, 54.74, 54.34]

serie_lanzamiento = pd.Series(lanzamiento, index=titulos)
serie_recaudaciones = pd.Series(recaudaciones, index=titulos)
serie_espectadores = pd.Series(espectadores, index=titulos)
recaud_ordenada = serie_recaudaciones.sort_values(ascending=False)
precio_entrada = recaud_ordenada / serie_espectadores
for pelicula in recaud_ordenada.index:
    print(f"{pelicula}: Es del {serie_lanzamiento[pelicula]}, "
          f"recaudó {recaud_ordenada[pelicula]} millones, "
          f"{serie_espectadores[pelicula]} millones de espectadores, "
          f"{precio_entrada[pelicula]:.2f}$ por entrada")
# Año de la película con menor recaudación
serie_lanzamiento[serie_recaudaciones.idxmin()]

# Película con más de 1000 millones y menos de 75 millones de espectadores
serie_recaudaciones[(serie_recaudaciones>1000) & (serie_espectadores<75)]

# Edad de Gonzalo al estreno
30 - (2023 - serie_lanzamiento)
serie_lanzamiento["Toy Story 4"] = 2019
serie_lanzamiento["Up"] = 2009
serie_recaudaciones["Monsters University"] = 754
serie_lanzamiento = serie_lanzamiento.rename({"Caco":"Coco"})
serie_recaudaciones = serie_recaudaciones.rename({"Caco":"Coco"})
serie_espectadores = serie_espectadores.rename({"Caco":"Coco"})
df = pd.DataFrame({
    "lanzamiento": serie_lanzamiento,
    "recaudacion": serie_recaudaciones,
    "espectadores": serie_espectadores,
    "Ingreso_por_espectador": serie_recaudaciones / serie_espectadores
})
# Por año ascendente
df_ordenado_ano = df.sort_values("lanzamiento")

# Por ingreso por espectador descendente
df_ordenado_ingreso = df.sort_values("Ingreso_por_espectador", ascending=False)
# Películas >10 años
df[df["lanzamiento"] <= 2013]

# Películas con recaudación>800 y espectadores>65
df[(df["recaudacion"]>800) & (df["espectadores"]>65)]
df_reset = df.reset_index().rename(columns={"index":"Peliculas"})
df_set_index = df_reset.set_index("lanzamiento")

```
