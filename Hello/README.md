# Hello - Gramática básica con ANTLR4

Este es el ejemplo más simple de ANTLR4. La gramática reconoce frases de la forma `hello nombre`, donde el nombre debe estar en minúsculas.

La gramática definida en `Hello.g4` es:

```antlr
grammar Hello;
r  : 'hello' ID ;
ID : [a-z]+ ;
WS : [ \t\r\n]+ -> skip ;
```

- `r` es la regla principal: espera la palabra `hello` seguida de un identificador.
- `ID` reconoce palabras en minúsculas.
- `WS` ignora los espacios.

---

## Paso 1 - Generar los archivos del parser y lexer

ANTLR lee la gramática y genera automáticamente los archivos Java necesarios para analizar el lenguaje.

```bash
antlr4 Hello.g4
```

Esto genera varios archivos `.java` como `HelloParser.java`, `HelloLexer.java`, entre otros. Estos ya están disponibles en la carpeta `antlr/`.

---

## Paso 2 - Compilar los archivos generados

Se compilan todos los `.java` incluyendo el `.jar` de ANTLR en el classpath:

```bash
javac -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar *.java
```

Esto genera los archivos `.class` que Java necesita para ejecutar el programa. Estos ya están disponibles en la carpeta `javac/`.

---

## Paso 3 - Probar la gramática

Con `grun` (la herramienta de prueba de ANTLR) se puede verificar que la gramática funciona correctamente.

**Ver el árbol de parseo en texto:**

```bash
grun Hello r -tree
```

Escribe una entrada válida y presiona `Ctrl+D`:

```
hello world
```

Resultado esperado:

```
(r hello world)
```

**Ver el árbol de parseo de forma gráfica:**

```bash
grun Hello r -gui
```

Escribe:

```
hello world
```

Presiona `Ctrl+D` y se abrirá una ventana con el árbol visual.

**Ver los tokens reconocidos:**

```bash
grun Hello r -tokens
```

Resultado esperado:

```
[@0,0:4='hello',<1>,1:0]
[@1,6:10='world',<2>,1:6]
[@2,12:11='<EOF>',<-1>,2:0]
```

---

## Capturas de ejecución

**Árbol de texto (`-tree`):**

<!-- Insertar captura aquí -->

**Árbol gráfico (`-gui`):**

<!-- Insertar captura aquí -->

**Tokens (`-tokens`):**

<!-- Insertar captura aquí -->
