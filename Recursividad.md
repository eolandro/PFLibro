## Recursividad

Recordando el contexto historico de los lenguajes funcionales, siendo lisp uno de los pioneros, la forma en la cual este lenguaje es turing completo es la recursividad. Es importante tener en cuenta que esta es heredada directamente de la inspiracion base de lisp, el calculo lambda de Alonzo Church. <sub>Poner ref a la autoreferencia y la recursividad</sub>

Esta es la razón por la cual la forma natural de iterar de muchos lenguajes funcionales y en general de muchos lenguajes declarativos es uso o abuso de la recursividad. 
No obstante, multiple bibliografia detalla que la recursividad se pude clasificar de la siguiente manera: 
* Directa. Cuando una funcion se llama asi misma dentro de su cuerpo de fucion. F => F
* Indirecta. Cuando una funcion se llama asi misma con el uso de una funcion auxiliar. F => P => F

<sub> Menciónar bibliografía concreta </sub>

Es produnte enunciar que las funciones recursivas deben cumplir dos caracteristicas principales:

* Llamada de expansión. Sentencia cuyo objetivo es realizar las llamadas autoreferenciadas de la función. Es de expansión, porqué cada llamada nueva agrega una copia de sus datos<sub>?</sub> a la pila de ejecución de la Máquina Virtual del Lenguaje o la pila de ejecución de la CPU, es decir la función se expande.

* Condición de colapso. También llamada de cierre o caso base, es una condición en la cual la función termina y comienza el proceso (o no) de cerrar las ejecuciones previas de si misma en la pila de ejecución, es decir la función colapsa.

Para cumplir con los objetivos del presente, se limitarán los ejemplos a *recursividad directa*.

Un ejemplo sencillo de recursividad es imprimir todos los números previos desde N hasta 0.

Veamos este ejemplo en python:

```python

def imprimir_anteriores(N):
    if N == 0: # Colapso
        print(N)
        return
    print(N)
    imprimir_anteriores(N-1) #expansion


```
Si se analiza el código, vemos que los comentarios ya nos indican donde está la condición de colapso y la sentencia de expansión. Para entender del funcionamiento, de las anteriores suponga que ejecutamos la función con el parámetro N = 0.
```
imprimir_anteriores(0)
0
```
Podemos generar la siguiente tabla al ejecutar instrucción por instrucción 
| Instrucción | Variables | Resultado |
|-------------|-----------|-----------|
|```if (N == 0):```| N -> 0 | True, entra en el if |
|```print(N)```| N -> 0 | Salida en consola "0" |
|```return```| N -> 0 | Termina función |
La función colapsa en N = 0, porque es el caso base de la función, * es recomendable comenzar siempre por el caso base *. No obstante en esta ejecución la función jamas se ha expandido, si queremos ver qué esto suceda. Tendremos que evaluar con N > 0, por ejemplo suponga N = 2
```
imprimir_anteriores(2)
2
1
0
```
La tabla de ejecución sería la siguiente:
| Instrucción | Variables | Resultado |
|-------------|-----------|-----------|
|```if (N == 0):```| N -> 2 | False, no entra al if |
|```print(N)```| N -> 2 | Salida en consola "2" |
|```imprimir_anteriores(N - 1)```| N -> 2 | Resta 2-1, expansión de la función|
|```if (N == 0):```| N -> 1 | False, no entra al if |
|```print(N)```| N -> 1 | Salida en consola "1" |
|```imprimir_anteriores(N - 1)```| N -> 1 | Resta 1-1, expansión de la función|
|```if (N == 0):```| N -> 0 | True, entra en el if |
|```print(N)```| N -> 0 | Salida en consola "0" |
|```return```| N -> 0 | Termina función |
|| N -> 1 | Termina función |
|| N -> 2 | Termina función |