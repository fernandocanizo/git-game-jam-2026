---
marp: true
style: |
  section.title-center {
    display: flex;
    flex-direction: column;
    justify-content: center;   /* vertical */
    align-items: center;       /* horizontal */
    text-align: center;
  }
---
<!-- _class: title-center -->

# Taller de git
# para videojuegos

---
<!-- _class: title-center -->

# Taller de git
# ~~para videojuegos~~

---
<!-- _class: title-center -->

## Por Fernando L. Canizo (aka Conan)

![qr-code](./img/talk-repo-qr-code.png)

---

## Preguntas antes de comenzar

* Levanten la mano quienes usan Windows
* Levanten la mano quienes usan Linux o similar: BSD, Mac, Unix.
* ¿Alguno ya ha usado git?
* Levanten la mano quienes programan
* Levanten la mano quienes diseñan, dibujan o hacen arte en general
* Levanten la mano los que no levantaron la mano

---
## Qué es git?

* Git es un sistema de control de versiones distribuido.

* Permite llevar un registro de los cambios realizados en el código fuente de un proyecto.

* Cada copia local del proyecto, se conoce como **repositorio**.
  (**repo** para los amigos).

* El repositorio contiene el historial completo, lo que permite trabajar sin
  conexión (SVN).

---

## Más sencillo

Git es una máquina del tiempo.

* volver atrás
* comparar
* probar
* **sin miedo**

---

## Por qué necesitamos control de versiones?

---

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
---

## Por qué necesitamos control de versiones?

### ¿Y ahora?
```
$ ls -1
proyecto-2026.01.30.txt
proyecto.txt
proyecto.final.txt
proyecto.final-final.txt
proyecto.final2.txt
```

---

## Por qué necesitamos control de versiones?

### La memoria humana es frágil

El control de versiones registra metainformación, por ejemplo:

* guarda decisiones
  _¿Por qué se modificó esto?_ _¿Por qué se hizo de tal manera?_
* registra intentos
  _Usé la biblioteca A, pero no funcionó, entonces cambié a B._
* conserva caminos descartados
  _Los usuarios estaban más contentos con la vieja manera de calcular puntaje_.

---

## Por qué necesitamos control de versiones?

* Código deshabilitado vía comentario
* ¿Qué hacemos si queremos recuperar una versión anterior y ya la hemos borrado?
* Equivocarse no debería ser catastrófico
* Irremplazable si se trabaja en equipo
* Respaldo automático

---
## ¿Para qué se puede usar git?

* **PARA TODO**
* guardar la configuración de mi entorno de shell y de algunas aplicaciones del mismo
* guardar la configuración de Neovim, mi editor
* guardar mis bookmarks
* guardar mis notas sobre tech stacks
* guardar cuentos que escribo
* guardar esta charla
* repositorio de tips sobre comandos que uso con poca regularidad

---
## Continuación...

* registro de libros que leo
* registro de mis claves usando la herramienta `pass`
* repositorio de scripts de shell utilitarios: privados y públicos
* ideas para juegos
* revisión de bibliotecas y herramientas
* repositorios de aprendizaje: siempre que aprendo alguna nueva tecnología o que sigo un tutorial, creo un repositorio
* mi perfil en github es un repositorio también
* etc...

---

## Estados en git

* **committed:** los cambios han sido guardados en la base de datos local de git.

* **modificado:** se ha cambiado algo, pero no se ha comiteado aún.

* **staged:** indica que has marcado ciertos cambios para sumarlos al próximo comit.

___

![areas](./img/areas.png)
___

## Archivos de texto vs binario

* ¿Alguien me puede dar una definición?

* La distinción entre archivo binarios o de texto es semántica, no física.
  **A nivel físico todos los archivos son binarios**.

---

### Veamos algunos ejemplos...

- less /usr/share/wallpapers
- less /etc/inputrc
- less /usr/share/man/man7/address_families.7.gz
- zless /usr/share/man/man7/address_families.7.gz
- man address_families

---

## Manos a la obra

### Convención

* `comando <archivo>` ⟶  **parámetro requerido**
* `comando [archivo]` ⟶  **parámetro optativo**.

---

### Instalación

Nope!

---

### Configuración

```
git config --global user.name "Tu nombre"
git config --global user.email "ejemplo@email.com"
```

---

### Dos maneras de iniciar un repositorio

* `git clone <uri>`
* `mkdir taller-git; cd taller-git; git init`

---

### Agregar archivos, ver estado

* `vi uno` # editamos...
* `git add uno`
* `git status`
* `git commit`
* `git status`

---

### Ver cambios no comiteados

* `vi uno`
* `git status`
* `git diff`

---

### Atajo para decidir que incluir

* `git commit -p`
* `git commit -p [archivo] [...]`

---

### Importancia del nombrado de commits

* ver log de proyecto real

---

### Importancia de la separación de tareas

---

### ¿Qué hemos hecho?

* `git log`
* `git log -p`

---

### Veamos los cambios ocurridos en un sólo archivo

* `vi dos`
* `git add dos`
* `git commit`
* `git log -p`
* `git log -p -- uno`

---

### Ramas: ¿qué son?

* Las ramas son líneas de trabajo paralelas, versiones alternativas del trabajo.

---

### Ramas: ¿para qué se usan?

* experimentar sin riesgo
* trabajar en una característica sin afectar el funcionamiento actual del proyecto
* permitir que varias personas trabajen a la vez

---

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

---

### Ramas: integrar todos los cambios de una rama

```
git checkout main
# git log
git merge mi-rama
# git log
```

---

### Ramas: eliminar

```
git branch -d mi-rama
```

Forzar eliminación:

```
git branch -D mi-rama
```

---

### Ramas: incorporar sólo algunos cambios de otra rama

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

---

## Deshacer cosas

* `git commit --amend`
* `git restore`
* `git reset`
* para cambios staged:
  `git reset HEAD [archivo]` / `git restore --staged <archivo>`
* para cambios aún no staged:
  `git checkout -- <archivo>` / `git restore <archivo>`
* tirar los últimos cambios a la basura:
  `git reset --hard HEAD`

---

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

---
<!-- _class: title-center -->

## Muchas gracias :)

![qr-code](./img/talk-repo-qr-code.png)

