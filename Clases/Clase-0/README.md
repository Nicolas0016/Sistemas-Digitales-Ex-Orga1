## Teorema de la división:
Sean $a$ y $b$ dos números enteros, con $b \neq 0$.

Existen $q$ y $r$ enteros con $0 \leq r < |b|$ tales que $a = b \cdot q + r$.

Además, $q$ y $r$ son únicos.

¿Cómo lo usamos?

$a = b \cdot q + r$

$a = (b \cdot q_1 + r_1) \cdot b + r$

$a = [(b \cdot q_2 + r_2) \cdot b + r_1] \cdot b + r$

Podemos continuar con la expresión hasta que $q_n < b$

$a = {[(b \cdot q_n + r_n) \cdot b + r_{n-1}] \cdot b + \dots + r_1} \cdot b + r$

Si distribuimos nos va a quedar:

$a = b^n \cdot q_n + r_n \cdot b^{n-1} + r_{n-1} \cdot b^{n-2} + \dots + r_1 \cdot b^0$

Representación posicional: 
Podemos ver que el primer elemento de cada producto es el que va a aparecer en los dígitos de nuestra representación posicional, donde:

$a = q_n \cdot b^{n+1}+  r_n \cdot b^{n} + r_{n-1} \cdot b^{n-1} + \dots + r_1 \cdot b +  r \cdot b^0$

Se puede escribir como:

$$
\begin{array}{|c|c|c|c|c|c|}
\hline
q_n & r_n & r_{n-1} & \dots & r_1 & r \\
\hline
\end{array}
$$

O de forma correcta incluyendo la base:
$(q_n r_n r_{n-1} \dots r_1 r)_b$
Ejemplo:

$$27 = 2 \cdot 10¹ + 7 \cdot 10⁰ = 1 \cdot 2³ + 0 \cdot 2² + 1 \cdot 2¹ + 1 \cdot 2⁰$$

$$27 = (27)_{10} = (11011)_2$$


Ejercitación:
Escribir los siguientes números en binario, octal y hexadecimal:
- 10
- 512

Respuesta:

- Binario: 
$$10 = 1 \cdot 2^3 + 0 \cdot 2^2 + 1 \cdot 2^1 + 0 \cdot 2^0 = (1010)_2$$
- Octal:
$$10 = 1 \cdot 8^1 + 2 \cdot 8^0 = (12)_8$$
- Hexadecimal:
$$10 = 1 \cdot 16^1 + 0 \cdot 16^0 = (A)_{16}$$

- Binario:
$$512 = 1 \cdot 2^9 + 0 \cdot 2^8 + 0 \cdot 2^7 + 0 \cdot 2^6 + 0 \cdot 2^5 + 0 \cdot 2^4 + 0 \cdot 2^3 + 0 \cdot 2^2 + 0 \cdot 2^1 + 0 \cdot 2^0 = (1000000000)_2$$
- Octal:
$$512 = 1 \cdot 8^3 + 0 \cdot 8^2 + 0 \cdot 8^1 + 0 \cdot 8^0 = (1000)_8$$
- Hexadecimal:
$$512 = 2 \cdot 16^2 + 0 \cdot 16^1 + 0 \cdot 16^0 = (200)_{16}$$


## Rango de representación:
La forma de computar el rango es aplicando el cálculo de **combinaciones cruzadas**, por ejemplo una tira de 4 dígitos:

$$(a_3 a_2 a_1 a_0)_b$$

Donde cada dígito puede tener valores entre $0$ y $b-1$, tiene un rango igual a::
$$b \cdot b \cdot b \cdot b = b^4$$

Por ejemplo si representamos nuestros datos como naturales de ocho dígitos en base 2 tenemos que:

$$2 \cdot 2 \cdot 2 \cdot 2 \cdot 2 \cdot 2 \cdot 2 \cdot 2 = 2^8 = 256$$
> Esto luego se conocerá como el rango de un entero sin signo en 8 bits, y va del 0 al 255.

## Overflow:
El overflow es un error que ocurre cuando se intenta representar un número que excede el rango de representación de un tipo de dato. Por ejemplo, para los 8 dígitos de base dos del ejemplo, la magnitud 27 es represnetable:

$$27 = (\textbf{00011011})_2$$

> Observar que completamos con ceros a la izquierda para completar los 8 dígitos, esto se conoce como **padding**.

Ahora la magnitud 770 no es representable por quedar fuera del rango overflow:

$$770 = (11\textbf{00000010})_2$$
> Precisamos 10 dígitos como mínimo para representar la magnitud en base 2.

## Tipos de datos:
Los datos tienen **información asociada** (valores de cada dígito) y un **tipo de dato** (naturales acotados). El tipo indica cómo interpretar la información, vincularla con una magnitud y qué operaciones realizar.

Utilizaremos los siguientes tipos de datos para representar números naturales y enteros (en binario):
+ Sin signo (unsigned): Representa números positivos
+ Signo + magnitud (sign-magnitude): Se usa el primer dígito (bit) para indicar el signo de la magnitud
+ Exceso $m$:  represento a $n$ como $m + n$.
De esta manera, estamos desplazando la ubicación de la magnitud asociada al cero del comienzo del rango de representación a la posición $m$. Los valores a la izquierda de $m$ representan números negativos.

Ejemplos de rangos de representación para datos de 3 bits. El rango es:

$$
\begin{array}{|c|c|c|c|c|c|c|c|}
\hline
v_0 & v_1 & v_2 & v_3 & v_4 & v_5 & v_6 & v_7 \\
\hline
\end{array}
$$

> v es el valor de cada dígito, y el subíndice es la posición del dígito.

Los datos del rango son siempre iguales, lo que va a cambiar van a ser las magnitudes asociadas a cada elemento. Los datos son: 
$$\begin{array}{|c|c|c|c|c|c|c|c|}
\hline
v_0 & v_1 & v_2 & v_3 & v_4 & v_5 & v_6 & v_7 \\
\hline
000 & 001 & 010 & 011 & 100 & 101 & 110 & 111 \\
\hline
\end{array}
$$

Las magnitudes asociadas al rango serán:

$$\begin{array}{|c|c|c|c|c|c|c|c|c|}
\hline
\text{Posición} & v_0 & v_1 & v_2 & v_3 & v_4 & v_5 & v_6 & v_7 \\
\hline
\text {Dato} & 000 & 001 & 010 & 011 & 100 & 101 & 110 & 111 \\
\hline
\text{Sin signo} & 0 & 1 & 2 & 3 & 4 & 5 & 6 & 7 \\
\hline
\text{Signo + magnitud} & 0 & 1 & 2 & 3 & -0 & -1 & -2 & -3 \\
\hline
\text{Exceso 2} & -2 & -1 & 0 & 1 & 2 & 3 & 4 & 5 \\
\hline
\end{array}
$$
> $m = 2$, entonces $n$ se representa como $m + n$. Por ejemplo, el número -1 se representa como $2 + (-1) = 1$, el número 0 se representa como $2 + 0 = 2$, el número 1 se representa como $2 + 1 = 3$, y así sucesivamente.

> Noten que para signo + magnitud hay dos datos asociados al cero (el valor está desnormalizado).

### Codificando números enteros a base binaria
+ Los positivos se representan igual
+ Para los números negativos la forma práctica de saber la forma en que vamos a representarlos es la siguiente:
    - Si n es la magnitud a representar y $d_3 d_2 d_1 d_0$ los cuatro digitos para representarlo en 4 bits, lo que haceremos es invertir de a uno (cambiar unos por ceros y ceros por unos) y sumar uno.
+ Por ejemplo -4 se representa como inv(4) + 1, en 5 bits: 
$$inv(01000)_2 + 1 = (10111)_2 + 1 = (11000)_2$$

Otra forma de represetnarlo, para los números negativos lo que se almacena es el complemento de ṅ, a partir de:
$$
ṅ = 2^k_{(10)} - n
$$
Donde n es la magnitud interpretada, ṅ el dato almacenado y k la cantidad de dígitos (o bits) utilizados para representar al número.

Ejemplo:

Quiero representar el númeor $-2_{(10)}$ con k = 3 dígitos binarios.
Entonces, $2^k_{(10)} = 2^3_{(10)} = 8_{(10)} = 1000_{(2)}$
Luego $2 = 1000_{(2)}$ donde 2 es el complemetno a 2 del número.

Escribimos el 2 en la base correspondiente:
$$\dot{2} = 1000_{(2)} - 2_{(10)} = 1000_{(2)} - 010_{(2)}$$
Finalmente $\boxed{\cdot{2} = 110_{(2)}}$

Codificando

En base 2, datos de 4 bits:

| | signo + magnitud | complemento a 2  | exceso a 15 |
|---|---|---|---|
| 3 | 0011 | 0011 | OVERFLOW |
|-2| 1010 | 1110 | 1101 |
|-8| OVERFLOW | 1000 | 0111 |

En base 2, datos de 8 bits:

| | signo + magnitud | complemento a 2  | exceso a 15 |
|---|---|---|---|
| 3 | **0**000 0**011** | 0000 **0011** | 0001 0010 |
|-2| **1**000 0**010** | 1111 **1110** | 0000 **1101** |
|-8| 1000 1000 | 1111 **1000** | 0000 **0111** |


Extendiendo la cantidad de bis de precisión:
+ Signo + Magnitud: Se extiende con 0's, pero el bit más significativo se mentiene indicando el signo.
+ Complemento a 2: se extiende con el valor del bit más significativo
+ Exceso a m: Se extiende siempre con 0's

Enteros como numerales binarios:
Sin signo.
Numeral(dato) $\to$ número que representa
$1111_{(2)} \to 15_{(10)}$
$1110_{(2)} \to 14_{(10)}$
$1101_{(2)} \to 13_{(10)}$
$1100_{(2)} \to 12_{(10)}$
...
$0100_{(2)} \to 4_{(10)}$
$0011_{(2)} \to 3_{(10)}$
$0010_{(2)} \to 2_{(10)}$
$0001_{(2)} \to 1_{(10)}$
$0000_{(2)} \to 0_{(10)}$

Para los numerales de 4 bits.

Signo + Magnitud:
El primer bit es el signo, los demás son el significado (la magnitud del número en valor absoluto)
numeral $\to$ número que representa
$1100_{(2)} \to -4_{(10)}$
$1011_{(2)} \to -3_{(10)}$
$1010_{(2)} \to -2_{(10)}$
$1001_{(2)} \to -1_{(10)}$
$1000_{(2)} \to -0_{(10)}$
$0000_{(2)} \to 0_{(10)}$
$0001_{(2)} \to 1_{(10)}$
$0010_{(2)} \to 2_{(10)}$
$0011_{(2)} \to 3_{(10)}$
$0100_{(2)} \to 4_{(10)}$
Para numerales de 4 bits.

Complemento a dos

Los numerales que representa positivos son iguales a los anteriores
Para los negativos, dado un $\cdot{n}$ negativo se representa escribiendo
$$\cdot{n} = 2^k - n \text{en notación sin signo}$$
$$\text{cuentas} \to \text{numeral} \to \text{número que representa}$$

$2⁴ + (-1) = 15 \to 1111_{(2)} \to -1_{(10)}$
$2⁴ + (-2) = 14 \to 1110_{(2)} \to -2_{(10)}$
$2⁴ + (-3) = 13 \to 1101_{(2)} \to -3_{(10)}$
$2⁴ + (-4) = 12 \to 1100_{(2)} \to -4_{(10)}$
$2⁴ + (-5) = 11 \to 1011_{(2)} \to -5_{(10)}$
$2⁴ + (-6) = 10 \to 1010_{(2)} \to -6_{(10)}$
$2⁴ + (-7) = 9 \to 1001_{(2)} \to -7_{(10)}$
$2⁴ + (-8) = 8 \to 1000_{(2)} \to -8_{(10)}$

$0111_{(2)} \to 7_{(10)}$
$0110_{(2)} \to 6_{(10)}$
$0101_{(2)} \to 5_{(10)}$
$0100_{(2)} \to 4_{(10)}$
$0011_{(2)} \to 3_{(10)}$
$0010_{(2)} \to 2_{(10)}$
$0001_{(2)} \to 1_{(10)}$
$0000_{(2)} \to 0_{(10)}$
para los numerales de 4 bits.

Exceso a m
El número n se representa como $m + n$
$\text{cuentas} \to \text{numeral} \to \text{número que representa}$

$5 + (10) = 15 \to 1111_{(2)} \to 10_{(10)}$
$5 + (9) = 14 \to 1110_{(2)} \to 9_{(10)}$
$5 + (8) = 13 \to 1101_{(2)} \to 8_{(10)}$
$5 + (7) = 12 \to 1100_{(2)} \to 7_{(10)}$
$5 + (6) = 11 \to 1011_{(2)} \to 6_{(10)}$
$5 + (5) = 10 \to 1010_{(2)} \to 5_{(10)}$
$5 + (4) = 9 \to 1001_{(2)} \to 4_{(10)}$
$5 + (3) = 8 \to 1000_{(2)} \to 3_{(10)}$
$5 + (2) = 7 \to 0111_{(2)} \to 2_{(10)}$
$5 + (1) = 6 \to 0110_{(2)} \to 1_{(10)}$
$5 + (0) = 5 \to 0101_{(2)} \to 0_{(10)}$
$5 + (-1) = 4 \to 0100_{(2)} \to -1_{(10)}$
$5 + (-2) = 3 \to 0011_{(2)} \to -2_{(10)}$
$5 + (-3) = 2 \to 0010_{(2)} \to -3_{(10)}$
$5 + (-4) = 1 \to 0001_{(2)} \to -4_{(10)}$
$5 + (-5) = 0 \to 0000_{(2)} \to -5_{(10)}$

> Para interpretear un valor, osea una tira de valores binarios o bits, es necesario conocer su tipo. Tipos distintos para un mismo valor determinan (potencialmente) distintas magnitudes.
Operaciones aritmético-lógicas:
Es importante comprender que hay atributos que nos interesa observar tanto de los **datos como de las operaciones**. Por ejemplo: 
+ **De los datos numéricos** si son negativos o pares
+ **De las operaciones** si los resultados se mantienen dentro del rango de representación

> El dato nos permite determinar propiedades del valor representado

Ejemplo, el complemento a 2 de un dato de 4 bits: 
$$
\begin{array}{|c|c|c|c|c|}
\hline
\text{Posición} & v_3 & v_2 & v_1 & v_0 \\
\hline 
\text{Interpretación} & \text{signo} & x & x & \text{paridad}\\
\hline 
\text{Negativo} & 1 & x & x & x\\
\hline 
\text{Positivo} & 0 & x & x & 0\\
\hline 
\end{array}
$$
