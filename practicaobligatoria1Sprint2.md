```python
ejer_2 = [1, 2, 3, 4, 5]

cuadrados = [x**2 for x in ejer_2]
cuadrados
ejer_3 = ["Un", "árbol", "binario", "es", "una", "estructura", "de",
          "un", "tipo", "particular", "a", "veces", "no", "es", "ni", "binario"]

duplicado = "un"
indices_un = [i for i, v in enumerate(ejer_3) if v.lower() == duplicado.lower()]

duplicado = "es"
indices_es = [i for i, v in enumerate(ejer_3) if v.lower() == duplicado.lower()]

duplicado = "binario"
indices_binario = [i for i, v in enumerate(ejer_3) if v.lower() == duplicado.lower()]

indices_un, indices_es, indices_binario
ejer_9 = (3, 20, 3, 47, 19, 3, 29, 45, 67, 78, 90, 3, 3, 5, 2, 4, 7, 9, 4, 2, 4, 3, 3, 4, 6, 7)

# 1. Cuántas veces se repite el 3
repeticiones_3 = ejer_9.count(3)

# 2. Tupla nueva desde posición 5 a 10
nueva_tupla = ejer_9[5:11]

# 3. Cuántos elementos tiene la tupla
longitud = len(ejer_9)

repeticiones_3, nueva_tupla, longitud
60 in ejer_9
# Tupla a lista
lista_9 = list(ejer_9)

# Tupla a set
set_9 = set(ejer_9)

# Tupla a diccionario usando índices
diccionario_9 = {i: ejer_9[i] for i in range(len(ejer_9))}

lista_9, set_9, diccionario_9
ejer_6 = {1: 11, 2: 22, 3: 33, 4: 44, 5: 55}

producto = 1
for valor in ejer_6.values():
    producto *= valor

producto
libro1 = {"titulo": "1984", "autor": "Orwell", "idioma original": "inglés", "año de publicación": 1949}
libro2 = {"titulo": "El Hobbit", "autor": "Tolkien", "idioma original": "inglés", "año de publicación": 1937}
libro3 = {"titulo": "Rayuela", "autor": "Cortázar", "idioma original": "español", "año de publicación": 1963}
libro4 = {"titulo": "Dune", "autor": "Herbert", "idioma original": "inglés", "año de publicación": 1965}

libreria = [libro1, libro2, libro3, libro4]
libreria
for libro in libreria:
    libro["idioma original"] = "esperanto"

libreria
titulo = "Dune"

coincidencias = [libro for libro in libreria if libro["titulo"].lower() == titulo.lower()]

if coincidencias:
    coincidencias
else:
    "Ese no lo tengo, ¿mola?"
def buscar_duplicados(lista, valor):
    return [i for i, v in enumerate(lista) if v.lower() == valor.lower()]

# Ejemplo
buscar_duplicados(ejer_3, "es")
def buscar_libro(libreria, titulo="ninguno"):
    coincidencias = [libro for libro in libreria if libro["titulo"].lower() == titulo.lower()]
    if coincidencias:
        return coincidencias
    else:
        return "Ese no lo tengo, ¿mola?"

# Ejemplo
buscar_libro(libreria, titulo="1984")
def validar_email(email):
    return "@" in email

email_usuario = input("Introduce tu email: ")

if validar_email(email_usuario):
    print("Email válido.")
else:
    print("Email inválido.")
def validar_dni(dni):
    letras = "TRWAGMYFPDXBNJZSQVHLCKE"
    
    if len(dni) not in (8, 9):
        return False
    
    numero = dni[:-1]
    letra = dni[-1].upper()

    if not numero.isdigit():
        return False

    numero = int(numero)
    letra_correcta = letras[numero % 23]

    return letra == letra_correcta

# Ejemplo
validar_dni("55555555P")

```


```python

```
