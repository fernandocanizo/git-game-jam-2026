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

### Más sencillo

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
## ¿Para qué se puede usar git? (1)

* **PARA TODO**
* guardar la configuración de mi entorno de shell y de algunas aplicaciones del mismo
* guardar la configuración de Neovim, mi editor
* guardar mis bookmarks
* guardar mis notas sobre tech stacks
* guardar cuentos que escribo
* guardar esta charla
* repositorio de tips sobre comandos que uso con poca regularidad

---
## ¿Para qué se puede usar git? (2)

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

* ver coloreado en Neovim al commitear
* ver log de proyecto real

---

### Importancia de la separación de tareas

---

### ¿Qué hemos hecho?

* `git log`
* ver archivos involucrados: `git log --raw --no-merges` (`list-changes`)
* `git log -p`
* versión reducida: `git log --oneline`

---

### ¿Qué son esos numerazos?

El hash SHA es la firma criptográfica del commit e incluye:

* el contenido del commit (los cambios)
* el mensaje del commit
* los commits padres hasta el inicio de la historia
* el timestamp
* algunos metadatos (cuyos detalles no conozco)

---

### Veamos los cambios ocurridos en un sólo archivo

* `vi dos`
* `git add dos`
* `git commit`
* `git log -p`
* `git log -p uno`

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

* `git branch`
* `git branch -c [base] <new branch>` and `git checkout <new branch>`
* `git checkout -b mi-rama` (topic branch / temática)
* `git branch`
* `vi tres`
* `git add tres`
* `git commit`
* `git log`

---

### Ramas: integrar todos los cambios de una rama

* `git checkout main`
* `git log`
* `git merge mi-rama`
* `git log`

---

### Ramas: eliminar

* Si no hay cambios no mergeados: `git branch -d mi-rama`
* Si queremos forzar descarte: `git branch -D mi-rama`

---

### Ramas: incorporar sólo algunos cambios de otra rama

* `git checkout -b otra-rama`
* `touch cuatro cinco seis`
* `git add cuatro`
* `git commit`
* `git add cinco`
* `git commit`
* `git add seis`
* `git commit`
* `git log`
* `git checkout main`
* `git cherry-pick <sha copiado de git log>`

---

## Deshacer cosas

* `git commit --amend`
* `git reset` / `git restore`
* para cambios staged:
  `git reset HEAD [archivo]` / `git restore --staged <archivo>`
* para cambios aún no staged:
  `git checkout <archivo>` / `git restore <archivo>`
* tirar los últimos cambios a la basura (staged o no): 
  `git reset --hard HEAD`
* deshacer un commit
  `git revert <sha>`

---

## Archivos binarios

- ver espacio usado por el proyecto
- agregar un archivo binario al directorio de trabajo
- ver espacio usado por el proyecto
- commitear
- ver espacio usado por el proyecto
- modificar imagen
- commitear
- ver espacio usado por el proyecto

---

## Trabajo en equipo (Parte 2?)

### [GitHub](https://github.com/)

Versión ultra-resumida e incompleta.

* `git clone <uri>`
* `git checkout dev`
* `git pull` (`fetch` ?)
* `git checkout -b nueva-rama-x`
* work, work, work..., commit, add...
* `git push`

---

### Alternativas a GitHub

* [GitLab](https://about.gitlab.com/): Open source, self-hosted, Docker.

* [BitBucket](https://bitbucket.org/): Atlassian. Jira/Trello.

* [Gitea](https://about.gitea.com/): Self-hosted.

* [SourceHut](https://sourcehut.org/): Choose-your-tool.

* [CodeBerg](https://codeberg.org/): Gratis. Community-driven. Requiere open-source.

* [Forgejo](https://forgejo.org/): Self-hosted. Obviamente, podés usar licencias privativas.

---

## Recursos de aprendizaje

* `git help`, `git help <command>`

* [Manual](https://git-scm.com/docs/user-manual)

* [Pro Git Book](https://git-scm.com/book/en/v2) por Scot Chacon y Ben Straub, editorial Apress, Creative Commons.

* [Manual en castellano](https://desarrolloweb.com/manuales/manual-de-git.html)
  No lo he usado, leí los contenidos, se ve piola.
  Artículos para tareas específicas.

* [Oh My Git!](https://ohmygit.org/)
  Juego.

---

## Interfaces gráficas

No uso. Pero hay mogollón.

---

## Cheatsheets

* [Reddit Coolguides](https://www.reddit.com/r/coolguides/comments/qmgm75/git_and_github_cheat_sheet/)

* [Reddit Git](https://www.reddit.com/r/git/comments/5m5fdz/git_cheat_sheet/)

---

## Bonus track

* `.gitignore`
* configuración: aliases
* configuración: usuario GitHub
* `tag`
* `mergetool` (`meld`)
* `stash`
* `rebase`
* `blame`
* `show`

---
<!-- _class: title-center -->

## Muchas gracias :)

![qr-code](./img/talk-repo-qr-code.png)

