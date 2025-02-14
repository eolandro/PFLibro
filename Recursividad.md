## Recursividad

Recordando el contexto historico de los lenguajes funcionales, siendo lisp uno de los pioneros, la forma en la cual este lenguaje es turing completo es la recursividad. Es importante tener en cuenta que esta es heredada directamente de la inspiracion base de lisp, el calculo lambda de Alonzo Church. <sub>Poner ref a la autoreferencia y la recursividad</sub>

Esta es la razón por la cual la forma natural de iterar de muchos lenguajes funcionales y en general de muchos lenguajes declarativos es uso o abuso de la recursividad. 
No obstante, multiple bibliografia detalla que la recursividad se pude clasificar de la siguiente manera: 
* Directa. Cuando una funcion se llama asi misma dentro de su cuerpo de fucion. F => F
* Indirecta. Cuando una funcion se llama asi misma con el uso de una funcion auxiliar. F => P => F

<sub> Menciónar bibliografía concreta </sub>

Para cumplir con los objetivos del presente, se limitarán los ejemplos a *recursividad directa*.

### Eje