# Temario

## Preguntas para conocer a mi público

- Qué sistema operativo usan?
  Si hay gente con Linux, la charla puede ser tipo taller y los oyentes podrían seguirme en lo que hago.
  Si no, entonces será una charla informativa más que nada y habrá que restarle énfasis a los ejemplos.

- Quiénes ya conocen y han usado git?
  Esta pregunta me puede servir para omitir algunos temas, como por ejemplo instalación y setup inicial.

## Tutorial / taller

### Qué es git?

Git es una herramienta que guarda localmente la historia de un trabajo, armando
en el proceso un versionado natural.

Recuerda absolutamente todos los cambios producidos en una obra, desde el
inicio. Es una memoria externa que registra cómo fue evolucionando la obra.

Eso permite volver atrás, comparar versiones y probar ideas nuevas sin miedo a
romper lo que existe.

## Por qué necesitamos control de versiones?

Todos hemos lidiado con el problema de versionar un trabajo cuando no estamos seguros de si realmente querremos mantener los cambios que hacemos o si tal vez deseemos volver a una versión anterior. Y aunque no nos interese mantener versiones, aún si estamos seguros que lo último que hicimos es lo que queremos entregar, queda el asunto de la nomenclatura de archivos: cómo se entera la persona a quien le entregamos, por ejemplo, un compañero, si es un trabajo conjunto, o el profesor si es un entregable del colegio o la facultad, que tal o cual archivo es el que corresponde usar para continuar el trabajo o para evaluar?

Posiblemente todos hayan pasado por la calamidad de creer que ya tenemos la versión final de algo, y luego hay que hacer un "último" cambio, y luego otro "último" cambio, y así nos quedamos con nombres de archivos como:

- proyecto.final
- proyecto.final2
- proyecto.final-final
- proyecto.final-final-otro
- ...

Y esta nomenclatura no tiene sentido. Cuál es el último?

### Estados en git

- **modificado:** se ha cambiado algo en el archivo, pero no se ha comiteado aún.

- **staged:** indica que has marcado un archivo modificado para sumarlo al próximo comit.

- **committed:** los cambios han sido guardados en la base de datos local de git.

(Voy a usar los términos en inglés, para mí no tiene sentido traducirlos)

![areas](/home/flc/Dropbox/my/cv/talks/2026.01.02,git-game.jam.2026/img/areas.png)

### Archivos de texto vs binario

La distinción entre archivo binarios o de texto es semántica, no física. A nivel físico todos los archivos son binarios.

No existe un método 100% seguro para determinar cual es cual, digamos, para explicarle a una máquina cual es cual y hacer que los identifique automáticamente, pero para un humano es bastante fácil: si podemos leerlo, aunque no entendamos lo que dice o lo que hace, es de texto. Y si vemos un montón de caracteres locos sin sentido, es binario.

#### Mostrar distintos archivos con vi o less

- /usr/share/wallpapers
- /etc/
- /usr/share/man/**/*.gz
  Acá, como son archivos comprimidos, tenemos las dos versiones del mismo contenido. Mostrar en crudo y con zless.

Esta distinción es importante para entender como funciona git debido a que git está pensado para trabajar con archivos de texto, guardando las diferencias que se producen línea a línea entre las distintas versiones de un archivo. Esas diferencias es lo que git guarda en su base de datos.

Mientras que cuando agregamos un archivo binario al repositorio, git no tiene manera de definir qué cambió, sólo sabe que ha sido modificado. Por lo tanto guarda el archivo completo en cada versión, lo cual es un tema a considerar cuando tenemos un repositorio de larga vida con muchos archivos binarios o bien muchas versiones de archivos binarios muy grandes.

## Manos a la obra

### Antes de empezar

Convención para la escritura de comandos: `comando <archivo>` un texto entre
símbolos menor y mayor indica que al comando se le debe pasar un parámetro, en
este caso un archivo. `comando [archivo]` un texto entre corchetes indica que
el comando soporta opcionalmente que se le pase un parámetro, pero no es
obligatorio dárselo.

### Ahora sí

- instalación
- configuración
- git init / git clone (lo veremos más adelante)
  Dos maneras de iniciar un repositorio para comenzar a trabajar.
- git add, git commit
  - Atajo: git commit -p
  - importancia del nombrado de commits
  - importancia de la separación de tareas
- git status
- git log
- ramas: para qué se usan y cómo

## Explorar alternativas

- git checkout -b
- git cherry-pick

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
