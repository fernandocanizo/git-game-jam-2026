# Temario

## Preguntas para conocer a mi público

- Qué sistema operativo usan?
  Si hay gente con Linux, la charla puede ser tipo taller y los oyentes podrían seguirme en lo que hago.
  Si no, entonces será una charla informativa más que nada y habrá que restarle énfasis a los ejemplos.

- Quiénes ya conocen y han usado git?
  Esta pregunta me puede servir para omitir algunos temas, como por ejemplo instalación y setup inicial.

## Qué es git?

Git es un sistema de control de versiones distribuido. Permite llevar un
registro detallado de los cambios realizados en el código fuente de un proyecto
a lo largo del tiempo. Cada copia local del proyecto, conocida como
repositorio, contiene el historial completo, lo que permite trabajar sin
conexión. 

Con git se puede volver a una versión anterior del proyecto, comparar y probar
ideas nuevas sin miedo a romper lo que existe.

## Por qué necesitamos control de versiones?

### ¿Cuál es el archivo a entregar?

```
$ ls -1
proyecto.final.txt
proyecto.final2.txt
proyecto.final-final.txt
proyecto.txt
proyecto-2026.01.30.txt
```

### ¿Y ahora?
```
$ ls -1
proyecto-2026.01.30.txt
proyecto.txt
proyecto.final.txt
proyecto.final-final.txt
proyecto.final2.txt
```

### Código deshabilitado vía comentario

### ¿Qué hacemos si queremos recuperar una versión anterior y ya la hemos borrado?

### La memoria humana es frágil

El control de versiones:
- guarda decisiones
- registra intentos
- conserva caminos descartados
- registra metainformación, por ejemplo:

  "¿Por qué se cambió esto y por qué se hizo así?"

### Equivocarse no debería ser catastrófico

### Irremplazable si se trabaja en equipo

### Respaldo automático

## Estados en git

- **modificado:** se ha cambiado algo en el archivo, pero no se ha comiteado aún.

- **staged:** indica que has marcado un archivo modificado para sumarlo al próximo comit.

- **committed:** los cambios han sido guardados en la base de datos local de git.

(Voy a usar los términos en inglés, para mí no tiene sentido traducirlos)

![areas](/home/flc/Dropbox/my/cv/talks/2026.01.02,git-game.jam.2026/img/areas.png)

## Archivos de texto vs binario

La distinción entre archivo binarios o de texto es semántica, no física. A
nivel físico todos los archivos son binarios.

No existe un método 100% seguro para determinar cual es cual, digamos, para
explicarle a una máquina cual es cual y hacer que los identifique
automáticamente, pero para un humano es bastante fácil: si podemos leerlo,
aunque no entendamos lo que dice o lo que hace, es de texto. Y si vemos un
montón de caracteres locos sin sentido, es binario.

### Veamos algunos archivos...

- less /usr/share/wallpapers
- less /etc/inputrc
- less /usr/share/man/man7/address_families.7.gz
- zless /usr/share/man/man7/address_families.7.gz
- man address_families

Esta distinción es importante para entender como funciona git debido a que git está pensado para trabajar con archivos de texto, guardando las diferencias que se producen línea a línea entre las distintas versiones de un archivo. Esas diferencias es lo que git guarda en su base de datos.

Mientras que cuando agregamos un archivo binario al repositorio, git no tiene manera de definir qué cambió, sólo sabe que ha sido modificado. Por lo tanto guarda el archivo completo en cada versión, lo cual es un tema a considerar cuando tenemos un repositorio de larga vida con muchos archivos binarios o bien muchas versiones de archivos binarios muy grandes.

## Manos a la obra

### Antes de empezar

Convención para la escritura de comandos: `comando <archivo>` un texto entre
símbolos menor y mayor indica que al comando se le debe pasar un parámetro, en
este caso un archivo. `comando [archivo]` un texto entre corchetes indica que
el comando soporta opcionalmente que se le pase un parámetro, pero no es
obligatorio dárselo.

### Instalación

### Configuración

```
git config --global user.name "Tu nombre"
git config --global user.email "ejemplo@email.com"
```

### Dos maneras de iniciar un repositorio para comenzar a trabajar

```
git init
```

```
git clone <uri>
```

### Agregar archivos al repositorio y ver estado del mismo

```
vi uno
git add uno
git status
git commit
git status
```

### Ver cambios no comiteados

```
vi uno
git status
git diff
```

### Atajo para decidir que incluir

```
git commit -p
```

### Importancia del nombrado de commits

### Importancia de la separación de tareas

### ¿Qué hemos hecho?

```
git log
git log -p
```

### Veamos los cambios ocurridos en un sólo archivo

```
vi dos
git add dos
git commit
git log -p
git log -p -- uno
```

### Ramas: ¿qué son?

Las ramas son líneas de trabajo paralelas, versiones alternativas del trabajo.

### Ramas: ¿para qué se usan?

Sirven para:

- experimentar sin riesgo
- trabajar en una característica sin afectar el funcionamiento actual del proyecto
- permitir que varias personas trabajen a la vez

### Ramas: ¿cómo?

```
# git branch
git checkout -b mi-rama
# git branch
vi tres
git add tres
git commit
# git log
```

### Incorporar los cambios de una rama

```
git checkout main
# git log
git merge mi-rama
# git log
```

### Incorporar sólo algunos cambios de otra rama

```
git checkout -b otra-rama
touch cuatro cinco seis
git add cuatro
git commit
git add cinco
git commit
git add seis
git commit
git log
git checkout main
git cherry-pick <sha copiado de git log>
```

## Deshacer cosas

- git commit --amend

- git restore
- git reset
- para cambios staged:
  git reset HEAD [archivo] / git restore --staged <archivo>
- para cambios aún no staged:
  git checkout -- <archivo> / git restore <archivo>
- tirar los últimos cambios a la basura: git reset --hard HEAD

## Trabajo en equipo

### GitHub

- git clone
- git pull / git fetch
- git push
- merge y rebase

### Alternativas a GitHub

- gitlab
- ...

## Recursos de aprendizaje

- `git help`, `git help <command>`
- [Manual](https://git-scm.com/docs/user-manual)
- [Pro Git Book](https://git-scm.com/book/en/v2) por Scot Chacon y Ben Straub, editorial Apress, bajo una licencia Creative Commons que permite compartirlo y adaptarlo.
- [Manual en castellano](https://desarrolloweb.com/manuales/manual-de-git.html)
  Lo encontré buscando recursos para pasarles, no lo he usado, sólo leí los contenidos, pero se ve bastante piola, con artículos específicos que explican tareas específicas que podrían surgir cuando uno usa git.
- [Oh My Git!](https://ohmygit.org/) (juego)

## Interfaces gráficas

Personalmente no uso interfaces gráficas, me resulta mucho más intuitivo trabajar con git desde el shell, sin embargo aquí les menciono algunas para los amantes del mouse:

TODO buscar clientes gráficos de git para linux, windows, mac
- VSCode (es con plugin o lo tiene nativamente?) TODO

## Cheatsheet

Les describo un posible flujo de trabajo compartido que uso desde hace años en mi trabajo.

TODO colocar comandos y breve descripción (cuando es la primera vez que aparecen) explicando lo que hace

## Bonus track

No tenía claro al diseñar el taller, el tiempo que nos tomaría, dado que no sabía si esto iba a ser un taller en que nos íbamos a ensuciar las manos o si iba a ser más bien una charla introductoria/demostrativa.

Si estamos viendo esto, es porque sobró tiempo ;)

- .gitignore
- configuración: alias
- tagueado
- mergetool
