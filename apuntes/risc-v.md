# Directivas de Ensamblador

## `.data`
Es una sección donde se declaran variables globales y constantes.
- Contiene variables inicializadas, constantes, cadenas de texto y vectores.
- Es una zona de lectura y escritura, por lo que se puede modificar durante la ejecución del programa.

**Ejemplo:**
```assembly
.data
    variable_global: .word 10
    cadena: .asciiz "Hola, mundo!"
    vector: .word 1, 2, 3, 4, 5
```

## `.text`
Es una sección donde las instrucciones del programa son declaradas.
- Contiene el código fuente y las instrucciones.
- Es una zona de solo lectura; no puede modificarse en tiempo de ejecución.

**Ejemplo:**
```assembly
.text
    # Declaración de instrucciones
    li t0, 10         # t0 = 10
    li t1, 20         # t1 = 20
    add t2, t0, t1    # t2 = t0 + t1
```

# Instrucciones Básicas

## `la` (Load Address)
Sirve para cargar la dirección de memoria de una variable global o constante en un registro.

**Ejemplo:**
```assembly
.data
    variable_global: .word 10

.text
    la t0, variable_global # t0 = &variable_global (dirección de memoria)
```

## `lw` (Load Word)
Sirve para cargar un valor (de 32 bits / 1 word) desde la memoria hacia un registro.

**Ejemplo:**
```assembly
.data
    variable_global: .word 10

.text
    la t0, variable_global # t0 = &variable_global (dirección de memoria)
    lw t1, 0(t0)           # t1 = variable_global
```

## `li` (Load Immediate)
Sirve para cargar un valor numérico constante (inmediato) en un registro.

**Ejemplo:**
```assembly
.text
    li t0, 10 # t0 = 10
```

## `addi` (Add Immediate)
Sirve para sumar un valor numérico constante a un registro.

**Ejemplo:**
```assembly
.text
    li t0, 10       # t0 = 10
    addi t0, t0, 5  # t0 = t0 + 5
```

## `beq` (Branch if Equal)
Compara dos registros y realiza un salto a una etiqueta si sus valores son iguales.

**Ejemplo:**
```assembly
.text
    li t0, 10
    li t1, 20
    beq t0, t1, etiqueta # si t0 == t1, saltar a etiqueta
```

## `j` (Jump)
Da un salto incondicional a una etiqueta.

**Ejemplo:**
```assembly
.text
    j etiqueta # saltar a la etiqueta indicada
```

# Ejercicio Integrador

**Enunciado:**
Se cuenta con un arreglo en memoria que contiene cuatro datos (words). Queremos iterar sobre ese arreglo, sumar el valor de los cuatro datos y almacenar el resultado en un registro. Escribir el programa en lenguaje ensamblador RISC-V que realice esta operación.

**Solución:**
```assembly
.data
    vector: .word 0x90, 0x1A, 0x00, 0x02
    longitud: .word 4
    
.text 
main: 
    # Guardo la posición en memoria del inicio del array
    la t0, vector
    lw t1, longitud # Contador de iteraciones
    li t2, 0        # Resultado acumulado de la suma

for:
    beq t1, zero, fin # Si el contador t1 es 0, salta a fin
    
    lw t3, 0(t0)      # Cargar el elemento actual del arreglo
    add t2, t2, t3    # Sumar el elemento al acumulador
    
    addi t0, t0, 4    # Siguiente posición en memoria (4 bytes por word)
    addi t1, t1, -1   # Decrementar contador
    j for             # Volver al inicio del bucle

fin:
    li a7, 10         # Código de llamada al sistema para Exit (RARS/MARS)
    ecall             # Terminar programa
```
