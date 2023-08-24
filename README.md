# Auxiliar 1: Git

Git es un software que permite hacer control de versiones de nuestros proyectos. Durante esta actividad vamos a simular un flujo de trabajo de desarrollo de software.

## Introducción

Los objetivos de esta actividad son los siguientes:

* Aprender a realizar commits utilizando los comandos de git.
* Resolver un conflicto en git cuando dos personas modifican un mismo archivo.
* Pasarlo bien.

Para esta actividad necesitarán:
1. Tener instalado un cliente de git, el cual pueden descargar y configurar siguiendo este [tutorial](https://docs.github.com/en/get-started/quickstart/set-up-git).
2. Contar con una segunda persona.
3. Su editor de texto favorito. Entre ellos están: [Sublime Text](https://www.sublimetext.com/blog/articles/sublime-text-4), [VS Code](https://code.visualstudio.com/).

## Actividad

### Parte 1: Fork del proyecto

Cada pareja trabajará sobre el mismo código base, pero deberan hacer una copia de este código en su repositorio personal, así, sus cambios no afectarán a otras parejas.

Una persona de la pareja (Persona A) debería hacer un "Fork de este repositorio (el que están viendo ahora). Para ello, en Github deberán hacer click en "Fork" y seguir las instrucciones. 

Luego de hacer el Fork, deberían tener un repositorio con la misma imagen con el nombre *sunombredeusuario/Auxiliar1-Git*. Esto implica que tendrán su propia versión del repositorio, en el cual podrán tener control de todo.

Ahora, la persona A (quien realizó el fork) deberá darle acceso a su pareja (Persona B). Para ello deberán ir a "settings" en la barra superior del repositorio (como indica la imágen).

![settings](https://i.imgur.com/fe4pMvn.png)

Luego, Collaborators -> Manage access -> Add people.

![add_people](https://i.imgur.com/TN1XT6I.png)

> Todos los miembros deben ser colaboradores del repositorio. Esto les dará acceso a hacer modificaciones al proyecto.

### Parte 2: Clonar el proyecto

Ahora, ambas personas deberán clonar el repositorio en sus computadoras siguiendo los siguientes pasos:

1. Clonar el enlace del repositorio. Para ello deberán copiar el enlace que aparece al presionar "<> Code", en la pestaña "HTTP" como indica la imágen.

![code](https://i.imgur.com/PXuKFxk.png)

2. Clonar el repositorio en sus computadoras utilizando la consola de Git: `git clone https://github...`

### Parte 3: Editar el proyecto

En este paso, cada integrante de la pareja hará un cambio en el proyecto, que no afectará el trabajo del otro y luego ambas personas descargarán los cambios.

1. **Persona 🅰️** editará el archivo `tarea.py`, agregando el siguiente método de clase:
```python
def terminar(self):
        self.listo = True
```

2. **Persona 🅰️** actualizará el repositorio remoto. Desde la consola de Git se deberá "empujar" los cambios que se hicieron. Para ello, debe hacer lo siguiente en la consola de git (situandola en la carpeta raíz del repositorio).

    + `git status` para ver qué cambios se hicieron.
    + `git add nombre-archivo` para agregar un archivo al commit. En este caso el archivo será tarea.py 
    + `git commit -m "descripción del cambio que se hizo" ` para hacer commit de los cambios. 
    + `git push` para subir los cambios al repositorio remoto.  

3. **Persona 🅱️**  editará el archivo `usuario.py`, y agregará los siguientes métodos de clase:

```python
def listarTareas(self):
    for tarea in self.tareas:
        if tarea.estaLista():
            print(f"[X] {tarea.obtenerNombre()}" )
        else:
            print(f"[ ] {tarea.obtenerNombre()}" )
```

4. **Persona 🅱️** actualizará el repositorio remoto con sus cambios según el paso 2. Al hacer `git push` aparecerá un mensaje de error.

Esto pasará porque **Persona 🅰️** hizo cambios a un archivos, cambios que **Persona 🅱️** no ha descargado. Para arreglar esto, **Persona 🅱️** deberá hacer `git pull`. Al hacer esto, juntará (merge) la versión del repostorio remoto con la versión local. Por esta razón aparecerá un editor con un mensaje parecido a este:

![]()

> Si no hay instrucciones para salir de ahí, prueba escribiendo ":wq" y luego presiona enter. Si no funciona, pide ayuda.

Persona B deberá hacer `git push` de nuevo para que sus cambios se suban al repositorio remoto.

5. **Persona A** hará `git pull` en la consola de Git y podrá ver los cambios realizados por Persona B sin problemas.

> Para no tener este problema, se recomienda realizar `git pull` antes de las instrucciones del paso 2, pero después de modificar el código, así te aseguras de arreglar cualquier error que pueda producirse entre el código remoto y tus cambios locales antes de crear el commit.

### Parte 4: Editar mismo archivo

¿Qué pasaría si persona B quiere quitarle el método listarTareas a la clase Usuario en `usuario.py` sin avisar y **Persona A decide moidificar la forma en que se muestran la lista de tareas?

1. Persona B quitará la línea de código en `usuario.py`

```python
def listarTareas(self):
    for tarea in self.tareas:
        if tarea.estaLista():
            print(f"[X] {tarea.obtenerNombre()}" )
        else: <<<<<<< Elimina esta
            print(f"[ ] {tarea.obtenerNombre()}" ) <<<<< y esta
```

2. Persona B actualizará el repositorio remoto segúin las instrucciones de la parte 3, páso 2.

3. Persona A (SIN DESCARGAR LOS CAMBIOS DE LA OTRA PERSONA) editará la siguiente línea del mismo archivo:

```python
def listarTareas(self):
    for tarea in self.tareas:
        if tarea.estaLista():
            print(f"[X] {tarea.obtenerNombre()}" )
        else:
            print(f"[ ] {tarea.obtenerNombre()}" )
```
 Lo reemplazará por:
 
 ```python
def listarTareas(self):
    for tarea in self.tareas:
        if tarea.estaLista():
            print(f"La tarea {tarea.obtenerNombre()} está lista")
        else: <<<<<<< Elimina esta
            print(f"La tarea {tarea.obtenerNombre()} no está lista")
```

4. Persona A actualizará el repositorio remoto según las instrucciones de la parte 3, paso 2. Al hacer `git push`, Persona A verá que hay un conflicto como pasó en la parte anterior. Para resolver esto se debe hacer git pull y aparecerá este mensaje:

![]()

Esto pasa cuando dos personas editan en mismo archivo del proyecto. Muchas veces Git puede solucionar estos conflictos automáticamente, pero otras veces la persona que realiza el push deberá decidir cuál será el código definitivo (luego de conversar con todo el equipo de desarrollo).

5. Persona A verá que su archivo `usuario.py está modificado y le agregaron algunas líneas. Lo primero que se ve es:

```python
   <<<<<<< HEAD 
        <codigo local>
    >>>>>>>> 
```

Donde HEAD representa la punta de la rama en la que se está trabajando. En este caso, como ya se creó el commit, HEAD será la versión del código que Persona A editó recién. El código que aparecerá en esta parté será la versión del código en conflicto de la rama local. Luego veremos lo  siguiente:

```python
     <codigo remoto>
>>>>>>> 17ed5a8a2f2b44e4daf2302d63f6a6b8163xxxxx
```

Por lo tanto, el código que aparecerá ahí será la versión del código de la rama remota. En este caso sería el código que subió Persona B. El número largo que aparecerá es el identificador del último commit remoto.

> Con esto, Git nos muestra dos versiones del código, y la persona que está desarrollando deberá decidir cuál será la versión definitiva. Cuidado con este tipo de procedimientos, ya que podrían eliminar trabajo de otras personas.

6. Persona A decidirá dejar su versión y no la de su pareja, por lo que eliminará todo el código que Git agregó incluyendo los síumbolos <, HEAD e identificadores de commit. Viendo los códigos del punto 5 debería quedar solo <codigo local>.

7. Finalmente, Persona A deberá subir el resultado del merge. Para ello debe:

     1. Volver a agregar los archivos modificados durante el merge haciendo `git add usuario.py`.
     2. `git commit` para hacer commit del merge. Aquí no es necesario poner -m y el mensaje porque se está haciendo merge.
     3. `git push` para terminar de subir los cambios locales y el arreglo de los conflictos.

Si revisan los commits en github verán que se crearon dos commits. Un commit por hacer merge de la rama remota y la local, y otro commit que representa los cambios que hizo Persona A.
