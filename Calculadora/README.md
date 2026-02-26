# Calculadora - Gramática con visitor en ANTLR4

Este ejemplo implementa una calculadora que evalúa expresiones matemáticas. A diferencia del ejemplo Hello, aquí se usa un **visitor** para recorrer el árbol y calcular los resultados.

La gramática definida en `LabeledExpr.g4` reconoce:
- Operaciones: suma `+`, resta `-`, multiplicación `*`, división `/`
- Paréntesis para agrupar expresiones
- Asignación de variables: `x = 5`
- Evaluación de expresiones: `3 + 4 * 2`

---

## Archivos del proyecto

| Archivo | Descripción |
|---|---|
| `LabeledExpr.g4` | La gramática que define el lenguaje de la calculadora |
| `Calc.java` | Punto de entrada del programa, lee la entrada y lanza el visitor |
| `EvalVisitor.java` | Recorre el árbol de parseo y calcula los resultados |

---

## Paso 1 - Generar los archivos del parser y lexer

ANTLR lee la gramática y genera los archivos Java necesarios:

```bash
antlr4 -visitor LabeledExpr.g4
```

Esto genera archivos como `LabeledExprParser.java`, `LabeledExprLexer.java`, `LabeledExprBaseVisitor.java`, entre otros. Estos ya están disponibles en la carpeta `antlr/`.

---

## Paso 2 - Compilar todos los archivos Java

Se deben compilar tanto los archivos generados por ANTLR como los archivos propios del proyecto (`Calc.java` y `EvalVisitor.java`). Es importante estar en la carpeta donde están todos los `.java`:

```bash
javac -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar *.java
```

El `*.java` compila todos los archivos de una vez. Si no hay errores, se generan los `.class` correspondientes.

---

## Paso 3 - Ejecutar la calculadora

A diferencia del ejemplo Hello, aquí no se usa `grun` sino que se ejecuta directamente la clase `Calc`.

**Opción A - Escribir las expresiones a mano:**

```bash
java -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar Calc
```

Escribe expresiones y presiona Enter después de cada una. Cuando termines, presiona `Ctrl+D`.

**Opción B - Usar un archivo de texto (más cómodo para probar varios casos):**

Crea un archivo `expresiones.txt` con las operaciones que quieras probar, una por línea:

```
3 + 4
10 * 2
15 / 3
10 - 4
(2 + 3) * 4
```

Luego ejecútalo pasando el archivo como argumento:

```bash
java -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar Calc expresiones.txt
```

Resultado esperado:

```
7
20
5
6
20
```

**Probar con variables:**

Las variables permiten guardar un valor con una letra y reutilizarlo en otras operaciones. Crea un archivo `variables.txt`:

```
x = 5
y = 3
x + y
x * y
```

```bash
java -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar Calc variables.txt
```

Resultado esperado:

```
8
15
```

> Nota: Las líneas de asignación como `x = 5` no imprimen nada, solo guardan el valor en memoria para usarlo después.

---

## Ejemplos de expresiones válidas

| Expresión | Resultado |
|---|---|
| `3 + 4` | `7` |
| `10 * 2` | `20` |
| `15 / 3` | `5` |
| `10 - 4` | `6` |
| `(2 + 3) * 4` | `20` |
| `x = 5` | (guarda x=5, no imprime) |
| `x + 3` | `8` (si x fue asignado antes) |

---

## Como funciona internamente

1. `Calc.java` toma la entrada y la pasa al lexer y parser generados por ANTLR.
2. El parser construye un árbol de parseo según las reglas de `LabeledExpr.g4`.
3. `EvalVisitor.java` recorre ese árbol y evalúa cada operación:
   - `visitAddSub`: suma o resta dos expresiones
   - `visitMulDiv`: multiplica o divide dos expresiones
   - `visitAssign`: guarda una variable en memoria
   - `visitId`: recupera el valor de una variable guardada

---

## Capturas de ejecución

**Compilacion de archivos:**

<img width="479" height="18" alt="image" src="https://github.com/user-attachments/assets/1976ab55-a31e-410a-b8e6-4de03d7ff113" />

<img width="642" height="52" alt="image" src="https://github.com/user-attachments/assets/3a4d884b-8360-4ed7-b0fc-67abb2af88e9" />

<img width="1155" height="591" alt="image" src="https://github.com/user-attachments/assets/91e6de48-f7a6-452c-9d1f-22a821b213e6" />


**Ejecucion con expresiones desde archivo de texto:**

<img width="535" height="156" alt="image" src="https://github.com/user-attachments/assets/9bd92652-f227-4e4e-8cda-04858326bfeb" />


<img width="639" height="119" alt="image" src="https://github.com/user-attachments/assets/27129ead-eb68-4b15-be6d-ebb63f163262" />


**Ejecucion con variables desde archivo de texto:**

<img width="551" height="123" alt="image" src="https://github.com/user-attachments/assets/985a4a0a-2b7a-42f9-97c5-d36cec68ace3" />


<img width="639" height="73" alt="image" src="https://github.com/user-attachments/assets/07f5f567-0c32-40a2-8156-32207db168bf" />


