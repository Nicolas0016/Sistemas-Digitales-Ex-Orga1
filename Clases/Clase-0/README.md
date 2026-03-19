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

