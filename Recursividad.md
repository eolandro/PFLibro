## Recursividad

Recordando el contexto histórico de los lenguajes funcionales, siendo Lisp uno de los pioneros, la forma en la cual este lenguaje es turing completo es la recursividad. Es importante tener en cuenta que esta es heredada directamente de la inspiracion base de Lisp, el calculo lambda de Alonzo Church. <sub>Poner ref a la autoreferencia y la recursividad</sub>

Esta es la razón por la cual la forma natural de iterar de muchos lenguajes funcionales y en general de muchos lenguajes declarativos es uso o abuso de la recursividad. 
Si revisamos bibliografia consolidada, está detalla que la recursividad se pude clasificar de la siguiente manera: 
* Directa. Cuando una funcion se llama asi misma dentro de su cuerpo de fucion. F => F
* Indirecta. Cuando una funcion se llama asi misma con el uso de una funcion auxiliar. F => P => F

<sub> Menciónar bibliografía concreta </sub>

Es produnte enunciar que las funciones recursivas deben cumplir dos caracteristicas principales:

* Llamada de expansión. Sentencia cuyo objetivo es realizar las llamadas autoreferenciadas de la función. Es de expansión, porqué cada llamada nueva agrega una copia de sus datos<sub>?</sub> a la pila de ejecución de la Máquina Virtual del Lenguaje o la pila de ejecución de la CPU, es decir la función se expande.

* Condición de colapso. También llamada de cierre o caso base, es una condición en la cual la función termina y comienza el proceso (o no) de cerrar las ejecuciones previas de si misma en la pila de ejecución, es decir la función colapsa.

Para cumplir con los objetivos del presente, se limitarán los ejemplos a *recursividad directa*.

### Python

Un ejemplo sencillo de recursividad es imprimir todos los números previos desde N hasta 0.

Veamos una implementación en python:

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
|```if N == 0:```| N -> 0 | True, entra en el if |
|```print(N)```| N -> 0 | Salida en consola "0" |
|```return```| N -> 0 | Termina función |

La función colapsa en N = 0, porque es el caso base de la función, *es recomendable comenzar siempre por el caso base*. No obstante en esta ejecución la función jamas se ha expandido, si queremos ver qué esto suceda. Tendremos que evaluar con N > 0, por ejemplo suponga N = 2.

```
imprimir_anteriores(2)
2
1
0
```
La tabla de ejecución sería la siguiente:
| Instrucción | Variables | Resultado |
|-------------|-----------|-----------|
|```if N == 0:```| N -> 2 | False, no entra al if |
|```print(N)```| N -> 2 | Salida en consola "2" |
|```imprimir_anteriores(N - 1)```| N -> 2 | Resta 2-1, expansión de la función|
|```if N == 0:```| N -> 1 | False, no entra al if |
|```print(N)```| N -> 1 | Salida en consola "1" |
|```imprimir_anteriores(N - 1)```| N -> 1 | Resta 1-1, expansión de la función|
|```if N == 0:```| N -> 0 | True, entra en el if |
|```print(N)```| N -> 0 | Salida en consola "0" |
|```return```| N -> 0 | Termina función |
|| N -> 1 | Termina función |
|| N -> 2 | Termina función |

Puede llegar a ser enajenante, las ultimas 2 filas, pero hay que recordar que cada ejecución de una función toma un nuevo lugar dentro de la pila de ejecución y este lugar será liberado hasta que la ejecución de dicha función termine.
Esto significa que cuando se llama a 'imprimir_anteriores(1)', existe una 'imprimir_anteriores(2)' que está en espera de que termine la primera, asi mismo cuando se llama 'imprimir_anteriores(0)', existe una 'imprimir_anteriores(1)' que tambien esta en espera. 
Cuando 'imprimir_anteriores(0)' finalmente termina su ejecución, 'imprimir_anteriores(1)' termina inmediatamente y  posteriormente 'imprimir_anteriores(2)' lo que libera la pila de ejecución.

### Javascript (EmacScript)

Siguiendo con el mismo ejemplo de imprimir todos los números previos desde N hasta 0.

```javascript

function imprimir_anteriores(N){
    if (N == 0){ // Colapso
        console.log(N);
        return;
    }
    console.log(N);
    imprimir_anteriores(N-1); //expansion
}

```
Se puede observar que la implementación del código no difiere tanto, esto es por que tanto Python como Javascript son lenguajes por asi decirlo *primos* y tienen una relación notable con lenguaje C. Obviamente instrucciones como 'print' e 'if' de python, debieron ser adecuadas por sus contrapartes correspondientes en Javascript. No obstante en escencia es el mismo algoritmo.  Tambien se han agregado comentarios de donde esta la llamada de expasión y la condicin de colapso, por lo que basicamente la explicacion aplicada en python es la misma. 

Supongamos que se ejecuta con N = 2.

```
imprimir_anteriores(2);
2
1
0
```

La tabla de ejecución seria la siguiente:

| Instrucción | Variables | Resultado |
|-------------|-----------|-----------|
|```if (N == 0){```| N -> 2 | false, no entra al if |
|```console.logt(N);```| N -> 2 | Salida en consola "2" |
|```imprimir_anteriores(N - 1);```| N -> 2 | Resta 2-1, expansión de la función|
|```if (N == 0){```| N -> 1 | false, no entra al if |
|```console.logt(N);```| N -> 1 | Salida en consola "1" |
|```imprimir_anteriores(N - 1);```| N -> 1 | Resta 1-1, expansión de la función|
|```if (N == 0){```| N -> 0 | true, entra en el if |
|```console.logt(N);```| N -> 0 | Salida en consola "0" |
|```return```| N -> 0 | Termina función |
|```}```| N -> 1 | Termina función |
|```}```| N -> 2 | Termina función |

Quiza una ventaja que tiene Javascript es que a diferecia de python aqui si se puede notar que las ultimas dos lineas cierran la ejecución de la función, porque estas corresponden a las '}' al final del código.
Otro aspecto a notar es el estilo de sintaxis que se ha aplicado, corresponde principalmente a Emacscript 6 e inferior, sin embargo esto  no implica que en los siguientes Temas no se use una sintaxis más moderna.

### Elixir

Al trasladar el ejemplo a Elixir tiene sus peculiaridades, recordemos que Python y Javascript son lenguajes esencialmente imperativos, pero Elixir es un funcional impuro, que si bien se detallara más adelante el porque de la pureza, implica que elixir maneja de manera natural al recursividad.
Del mismo modo, se está considerando que Elixir pueda ser un lenguaje ajeno, por lo que en esta ocasión el ejemplo será un poco más explicativo.

```elixir
defmodule Recursividad do # Definición de modulo
    def imprimir_anteriores(0) do # Colapso
        IO.puts(0)
    end
    def imprimir_anteriores(n) do
        IO.puts(n)
        imprimir_anteriores(n-1) # Expansion
    end
end
```
En elixir las funciones se definen dentro de un modulo, en este caso se llama *Recursividad*, Aqui lo que llama la atención es que la función imprimir_anteriores se define 2 veces y eso es porque elixir usa *pattern matching*, esta caracteristica es heredada de su lenguaje padre *erlang*. No obstante cada una de estas definiciones corresponde tanton a la condicion de colapso, como a la llamada de expansion, para ver su funcionamiento vamos a ejecutar nuestro codigo y analizar la tabla de ejecución.

Sigue las estas instrucciones para ejecutar el código en elixir:

1. Primero es necesario guardar el codigo anterior en un archivo llamado *recursividad.exs*, es importante que este en minusculas.
2. Abre el interprete de comandos en la carperta donde hayas guardado a *recursividad.exs*.
3. Ejecuta el comando ```iex -r recursividad.exs``` deberias ver al como lo siguiente:
```
iex -r recursividad.exs
Erlang/OTP 27 [erts-15.1.2] [source] [64-bit] [smp:2:2] [ds:2:2:10] [async-threads:1] [jit:ns]

Interactive Elixir (1.18.0-dev) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```
4. Escribe la llamada a la funcion con parametro N = 2.

```elixir
iex(2)> Recursividad.imprimir_anteriores(2)
2
1
0
:ok
```

El *pattern matching* o coicidencia de patrones es una tecnica en la cual una expresión puede ser usada como una comparación y asignación al mismo tiempo, quiza un ejemplo similar seria el siguiente codigo en Javascript. ```if (a = true) {console.log('yei');}``` Aqui la variable 'a' le es asignado el valor de true, para entonces ser evaluada como cuerpo del if.

