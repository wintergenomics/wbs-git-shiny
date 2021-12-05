---
output:
  pdf_document: default
  html_document: default
---

# Git

¿Qué es Git? Git es un software de control de versiones distribuido y desarrollado por Linus Torvalds, para optimizar el trabajo en proyecto que cuenten con un gran número de archivos.

## Instalación de Git

### Linux

Si estás en `Fedora` puedes utilizar `yum`: 


```r
yum install git
```

Si tu Sistema operativo está basado en `Debian`como `Ubuntu` puedes usar `apt-get` o `apt`. 


```r
sudo apt-get install git
```

### macOS

Existen diversas opciones para instalar Git en macOS que puedes revisar [aquí] (https://git-scm.com/download/mac).

### Windows

Para instalar Git en Windows, revisa el siguiente [link](https://git-scm.com/download/win
).

## Trabajando con Git en la terminal

### Version de Git
Conocer versión de Git, escribe en tu terminal: 


```r
git --version
```

### Editar valores de configuración

Es importante revisar los espacios, mayúsculas y minúsculas. 

Ingresar tu nombre de usuario entre comillas `"`

```r
git config --global user.name "User name"
```

Ingresar tu correo electrónico: 

```r
git config --global user.email "myemail@example.com"
```

Revisa los valores de configuración 

```r
git config --list
```

### Pidiendo ayuda
Para pedir ayuda, usamos el comando `help` de las siguientes maneras

```r
git help config
```


```r
git config --help
```

### Comandos de apoyo para manejo de archivos desde terminal 
* `cd` - Cambiar de directorio de trabajo
* `ls` - Listar lo que hay en un directorio
* `clear`- Limpiar la terminal 
* `pwd` - Conocer la ruta de nuestro directorio de trabajo

## Trabajar con repositorio

### Iniciar un repositorio
Para iniciar un repositario usamos `init`

```r
git init
```

### Revisar el estatus de un repositorio
Para iniciar un repositario usamos `status`

```r
git status
```

### Agregar archivos
Para agregar aarchivos a un repositario usamos `add`


```r
git add -A
```

También podemos agregar archivos individuales

```r
git add .gitignore
```

### Eliminando archivos del área de preparación 
Para eliminar archivos, usamos `reset` seguido del nombre del archivo que queremos eliminar.

```r
git reset nombre_archivo.txt
```

### Agregando comentarios
Para agregar comentarios, usamos `commit` y ponemos entre comillas `"`el comentario que deseamos agregar.

```r
git commit -m "Mi primer comentario"
```

## Clonar un repositorio de GitHub
**Importante**: Para éste paso ya debes tener tu cuenta de [GitHub](https://github.com/).


```r
git clone url_del_repositorio_de_github
```

### Creando una rama (*branch*)
Usamos `branch`

```r
git branch -a
```

### Mostrar los cambios de un repositorio 
Usamos `diff`

```r
git diff
```

### Enviar cambios a repositorio remoto
Para enviar cambios a un repositorio remoto usamos `push` como se indica:

```r
git push origin main
```

### Trabajar sobre una rama (*branch*)
Para trabajar sobre una rama en particular, usamos `branch` seguido de la rama sobre la cual queremos trabajar

```r
git branch rama_prueba
```

Para guardar cambios en la rama , usamos `push` y `origin` seguido del nombre de la rama 


```r
git push -u origin rama_prueba
```

### Fusionar ramas
Si queremos unir dos ramas, usamos `merged`


```r
git branch --merged
```

### Eliminar una rama
Para eliminar una rama usamos `branch -d`seguido del nombre de la rama que queremos eliminar.

```r
git branch -d rama_prueba
```

También podemos usar:

```r
git push origin --delete rama_prueba
```

### Ver los cambios en ramas
Para ver los cambios en las ramas usamos `branch -a`

```r
git branch -a
```

