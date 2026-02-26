Configuración General para usar ANTLR

<img width="627" height="87" alt="image" src="https://github.com/user-attachments/assets/eceabfb9-1cac-4e76-8aae-0ec28efb5ea1" />

Se descarga ANTLR desde https://www.antlr.org/download.html

Se declaran alias para mayor comodidad:
nano ~/.bashrc

Se agrega lo siguiente al final del archivo:

alias antlr4='java -jar /home/zorin/antlr-4.13.2-complete.jar'
alias grun='java -cp .:/home/zorin/antlr-4.13.2-complete.jar org.antlr.v4.gui.TestRig'

Nota: La ruta varía dependiendo de donde se encuentre el archivo .jar

Se guarda con Ctrl+O → Enter → Ctrl+X

Para aplicar los cambios:
source ~/.bashrc

Para verificar que todo se hizo correctamente:
antlr4

