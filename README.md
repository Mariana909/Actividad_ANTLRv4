#  Configuración General para usar ANTLR4

##  Requisitos previos

### Java
ANTLR4 requiere tener **Java instalado**. Para instalarlo en Linux (Ubuntu/Zorin/Debian):

```bash
sudo apt update
sudo apt install default-jdk
```

Para verificar que Java quedó instalado correctamente:

```bash
java -version
```

Deberías ver algo como:
```
openjdk version "17.0.x"
```

---

##  Instalación de ANTLR4

Descarga el archivo `.jar` desde la página oficial:

 [https://www.antlr.org/download.html](https://www.antlr.org/download.html)
 <img width="627" height="87" alt="image" src="https://github.com/user-attachments/assets/0269e6d0-fdee-4e1c-b450-0974aae85a35" />


---

##  Configuración de alias

Para mayor comodidad, se declaran alias en el archivo de configuración de la terminal:

```bash
nano ~/.bashrc
```

Agrega lo siguiente al **final del archivo**:

```bash
alias antlr4='java -jar /home/tuUsuario/antlr-4.13.2-complete.jar'
alias grun='java -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar org.antlr.v4.gui.TestRig'
```

> **Nota:** Reemplaza `/home/tuUsuario/` con la ruta donde guardaste el archivo `.jar`. Para conocer tu usuario puedes ejecutar `whoami`.

Guarda el archivo con:
```
Ctrl+O → Enter → Ctrl+X
```

---

##  Aplicar los cambios

```bash
source ~/.bashrc
```

---

##  Verificar la instalación

```bash
antlr4
```

Si todo está correcto, debería mostrarse la ayuda de ANTLR4 como en la siguiente imagen:

![ANTLR4 funcionando](https://github.com/user-attachments/assets/eceabfb9-1cac-4e76-8aae-0ec28efb5ea1)

---

##  Uso básico

### 1. Generar archivos Java desde una gramática
```bash
antlr4 TuGramatica.g4
```

### 2. Compilar los archivos generados
```bash
javac -cp .:/home/tuUsuario/antlr-4.13.2-complete.jar *.java
```

### 3. Probar la gramática
```bash
# Ver árbol de texto
grun TuGramatica reglaInicial -tree

# Ver árbol gráfico
grun TuGramatica reglaInicial -gui

# Ver tokens
grun TuGramatica reglaInicial -tokens
```

>  Escribe tu entrada y presiona `Ctrl+D` para terminar.
