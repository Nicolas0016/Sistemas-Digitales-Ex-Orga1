# .data
Es una sección donde se declaran variables globales y constantes.
+ Contiene variables inicializadas, constantes, cadenas de texto y vectores
+ Es una zona de lectura y escritura, por lo que se puede modificar durante la ejecución del programa

Ejemplo
```assembly
.data
    variable_global: .word 10
    cadena: .asciiz "Hola, mundo!"
    vector: .word 1, 2, 3, 4, 5
```

# .text
Es una sección donde se declaran las instrucciones del programa.
+ Contiene las instrucciones del programa
+ Es una zona de solo lectura, por lo que no se puede modificar durante la ejecución del programa

Ejemplo
```assembly
.text
    # Declaración de instrucciones
    li $t0, 10 # $t0 = 10
    li $t1, 20 # $t1 = 20
    add $t2, $t0, $t1 # $t2 = $t0 + $t1
```

# la
Me sirve para cargar la dirección de memoria de una variable global o constante en un registro.

Ejemplo
```assembly
.data
    variable_global: .word 10

.text
    la t0, variable_global # t0 = &variable_global (direccion de memoria)
```
# lw
Me sirve para cargar el valor de una variable global o constante en un registro.

Ejemplo
```assembly
.data
    variable_global: .word 10

.text
    la t0, variable_global # t0 = &variable_global (direccion de memoria)
    lw t1, (t0) # t1 = variable_global
```

# li
Me sirve para cargar un valor inmediato en un registro.

Ejemplo
```assembly
.text
    li t0, 10 # t0 = 10
```
# addi
Me sirve para sumar un valor inmediato a un registro.

Ejemplo
```assembly
.text
    li t0, 10 # t0 = 10
    addi t0, t0, 5 # t0 = t0 + 5
```

# beq
Me sirve para comparar dos registros y saltar a una etiqueta si son iguales.

Ejemplo
```assembly
.text
    li t0, 10 # t0 = 10
    li t1, 20 # t1 = 20
    beq t0, t1, etiqueta # si t0 == t1, saltar a etiqueta
```

# j
Me sirve para saltar a una etiqueta.

Ejemplo
```assembly
.text
    j etiqueta # saltar a etiqueta XD 
```

Ejercicio donde uso varios:

Se cuenta con cuatro datos sin signo de un byte cada uno almacenados en el registro t0 y queremos sumar el valor de los cuatro datos. Escribir un programa en lenguaje ensamblador RISC-V que realice esta operaci´on y almacene el resultado en el registro t0.
Solucion:

```assembly
.data
    vector: .word 0x90, 0x1A, 0x00, 0x02
    longitud: .word 4
    
.text 
main: 
    # Guardo la posicion en memoria del inicio del array
    la t0, vector
    lw t1, longitud # Contador 
    li t2, 0        # Resultado de la suma

for:
    beq t1, zero, fin # Si t1 es 0, salta a fin
    
    lw t3, 0(t0)      # Cargar elemento
    add t2, t2, t3    # Sumar
    
    addi t0, t0, 4    # Siguiente posición
    addi t1, t1, -1   # Decrementar contador
    j for             # Volver al inicio del bucle (Corregido el nombre)

fin:
    li a7, 10         # Código de salida en muchos simuladores (como RARS/MARS)
    ecall             # Terminar programa
``

