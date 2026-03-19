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