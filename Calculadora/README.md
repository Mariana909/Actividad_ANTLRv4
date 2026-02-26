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
antlr4 LabeledExpr.g4
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

A diferencia del ejemplo Hello, aquí no se usa `grun` sino que se ejecuta directamente la clase `Calc`. La calculadora lee desde la entrada estándar línea por línea.

```bash
java -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar Calc
```

Escribe expresiones y presiona Enter después de cada una. Cuando termines, presiona `Ctrl+D`:

```
3 + 4
10 * 2
x = 5
x + 3
(2 + 3) * 4
```

Resultado esperado:

```
7
20
8
20
```

> Nota: Las asignaciones como `x = 5` no imprimen nada, solo guardan el valor en memoria.

---

## Ejemplos de expresiones válidas

| Expresión | Resultado |
|---|---|
| `3 + 4` | `7` |
| `10 * 2` | `20` |
| `15 / 3` | `5` |
| `10 - 4` | `6` |
| `(2 + 3) * 4` | `20` |
| `x = 5` | (guarda x=5) |
| `x + 3` | `8` |

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

<!-- Insertar captura aquí -->

**Ejecucion con expresiones simples:**

<!-- Insertar captura aquí -->

**Ejecucion con variables:**

<!-- Insertar captura aquí -->
