# Ejercicio 1

¿Qué es una arquitectura?¿Qué componentes la conforman?¿Contiene iformación del funcionamiento interno de las operaciones?

La arquitectura de un procesarodr se refiere a aquello con lo que podemos trabajar cuando escribimos un programa. Son instrucciones, los registros y forma de acceder a memoria, definiendo así la estructura lógica y comportamental del procesador.

Los componentes que la conforman son:

- Conjunto de instrucciones
- Conjunto de registros
- La forma de acceder a memoria

No contiene información del funcionamiento interno de las operaciones, es decir, no nos dice como está implementado el procesador.

# Ejercicio 2

1. ¿A cuántos bytes se direcciona la memoria en la arquitectura `RISC-V`? ¿Cuántos bytes hay en una palabra?

> Nota: un byte son 8 bits.

2. Sabiendo que la memoria se encuentra en el estado que se ve a continuación, indicar el resultado de las siguientes operaciones sabiendo que `t0 = 0xAD`.

| Direccion | ... | 0xAA | 0xAB | 0xAC | 0xAD | 0xAE | 0xAF | 0xB0 | 0xB1 | 0xB2 | ... |
| --------- | --- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
| Valor     | ... | 0x34 | 0x11 | 0xF4 | 0x09 | 0x12 | 0x73 | 0x20 | 0x24 | 0xFF | ... |

1. lw t1, 0(t0)
2. lw t1, 2(t0)
3. sw t1, -3(t0)
4. lh t1, -1(t0)
5. lhu t1, -1(t0)
6. lb t1, 5(t0)
7. lbu t1, 5(t0)

---
1. Los bytes que se direcciona la memoria en la arquitectura `RISC-V` son 2^32 bytes. En una palabra hay 4 bytes.

2. 
> lw: load word (carga 4 bytes) es igual a `a = memoria[x]`
> sw: store word (guarda 4 bytes) es igual a `memoria[x] = a`

> lh: load halfword (carga 2 bytes) 
Si el procesador lee 0xFFF0 de la memoria
Como es la instrucción lh, el procesador mira el bit más significativo (el de la izquierda). En 0xFFF0 el bit más significativo es 1, lo que indica que el número es negativo.
si el registro es x10 es el de 32 bits, el resultaod final será 0xFFFFFFF0, se rellenaros los 16 bits superiores con 1 para mantener el valor de -16 en 32 bits.


> lhu: load halfword unsigned (carga 2 bytes sin signo)
> lb: load byte (carga 1 byte)
> lbu: load byte unsigned (carga 1 byte sin signo)
> k(s3) con $k \in Z$ indica la direccion de memoria y s3 indica el registro que contiene el desplazamiento.

---
# Ejercicio 3
Dado el siguiente arreglo de enteros de 16 bits en el lenguaje java:

```java
int[] arreglo16b = {-1, 170, 255, -255, 0, 32, 10000, 0};
```

| Valor Decimal| Hexadecimal | Representación en memoria |
|--------------|-------------|---------------------------|
| -1 | 0xFFFF | FF FF |
| 170 | 0x00AA | AA 00 |
| 255 | 0x00FF | FF 00 |
| -255 | 0xFF01 | 01 FF |
| 0 | 0x0000 | 00 00 |
| 32 | 0x0020 | 20 00 |
| 10000 | 0x2710 | 10 27 |


Sabiendo que este arreglo se guarda en memoria empezando en la dirección 0xCC.

1. Dibujar el estado de la memoria
2. Si t0 = 0xCC, escribir un programa que dado un indice i, devuelve arreglo16b[i].

---
1. 

| Direccion | ... | 0xCC | 0xCD | 0xCE | 0xCF | 0xD0 | 0xD1 | 0xD2 | 0xD3 | 0xD4 | 0xD5 | 0xD6 | 0xD7 | 0xD8 | 0xD9 | 0xDA | 0xDB | ... |
| --------- | --- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | --- |
| Valor     | ... | FF   | FF   | AA   | 00   | FF   | 00   | 01   | FF   | 00   | 00   | 20   | 00   | 10   | 27   | 00   | 00   | ... |