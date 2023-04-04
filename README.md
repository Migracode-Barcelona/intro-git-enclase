# Tu segunda clase - Git y Github
**:warning: Como estás usando GitHub Education y CodeSpaces, algunas partes de esta lección, como establecer tu configuración de usuario, pueden no ser necesarias.**
## Objetivos de aprendizaje

Al final de esta clase, deberías ser capaz de:

* Explicar qué es Git y por qué es una herramienta útil.
* Obtener una copia de tus preguntas de tarea en tu ordenador.
  * (Para _clonar_ un repositorio).
* Guarda tus respuestas y envíalas a nuestros voluntarios.
  * (Para _commit_, _fork_ un repositorio, y _push_ cambios).
* Ver y responder a los comentarios sobre tu tarea.
  * (Para utilizar los flujos de trabajo _pull request_ de GitHub, y _push_ más cambios).
* Explorar cómo ha cambiado un archivo a lo largo del tiempo.
  * (Para usar el _history log_ de Git).

### Empezar

Usaremos Git como nuestro Sistema de Control de Versiones (también conocido como Control de Fuentes). En pocas palabras, un sistema de control de versiones toma instantáneas de tus archivos y las guarda.

> **¿Qué es el "control de versiones"?** El control de versiones es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, de forma que puedas recuperar versiones específicas más adelante.
> Le permite revertir archivos a un estado anterior, revertir todo el proyecto a un estado anterior, comparar los cambios en el tiempo, ver quién modificó por última vez algo que podría estar causando un problema, quién introdujo un problema y cuándo, y mucho más. Utilizar un VCS también significa que, si se estropean las cosas o se pierden archivos, se pueden recuperar fácilmente. Además, todo esto sale muy barato.

(Extracto de [Git Pro book](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) )

¿Qué es **Git**? Git es uno de los muchos Sistemas de Control de Versiones disponibles, y con diferencia [el más popular](http://stackoverflow.com/insights/survey/2015#tech-sourcecontrol).

¡No confundas Git con **GitHub**! GitHub es un sitio web muy popular donde puedes publicar y compartir tu código. Subes tu código como repositorios Git (un tipo de carpeta o directorio), para poder compartirlo. Esto hace posible colaborar con otras personas: todo el mundo escribe código que es rastreado por Git y se añade al mismo repositorio.

![](<.contenido/imagen (187).png>)

Durante nuestro curso, utilizaremos [GitHub](https://github.com/) para almacenar nuestro código. GitHub es el servicio Git más popular que existe, y es utilizado por muchas grandes empresas, como Facebook, Airbnb y The Guardian.

La mayoría de los ingenieros de software utilizan una herramienta llamada Git para organizar su código y colaborar con otras personas.

Git es una herramienta de control de versiones que se utiliza para mantener el historial de cambios. I - this sets up the remote URL (GitHub)t makes collaboration easier. Veremos muchos de sus usos a lo largo del curso.

Cada semana, vas a utilizar Git para obtener una copia de tus ejercicios de tarea, para enviar tus soluciones, y para obtener retroalimentación sobre tus soluciones. Hoy, vas a aprender cómo hacer estas cosas.

[Página GitHub de MigraCode >](https://github.com/migracode-barcelona)

Si Git no está instalado, sigue este tutorial de GitHub para [configurar Git](https://docs.github.com/en/github/getting-started-with-github/set-up-git#setting-up-git)

Una vez instalado Git, configura tu nombre de usuario y dirección de correo electrónico: `git config --global user.name <nombre>` y `git config --global user.email <email>`. Ejemplo:

```
git config --global user.name "Mona Lisa"
git config --global user.email email@example.com
```

**Git en el Terminal: comandos más usados**

* `git init` para ser usado sólo _**si es un proyecto nuevo**_, es decir, un proyecto no **clonado** desde un repositorio o un fork
* `git add .` para añadir archivos locales al **índice**.
* `git commit -m "Buena explicación de los cambios en tus archivos"` para enviar archivos al repositorio local
* `git remote add origin GitRepoRemoteUrl` para ser usado sólo _**si es un proyecto nuevo**_
* `git remote -v` para verificar que la URL remota está configurada correctamente
* `git push -u origin master` para enviar tus commits a la URL remota (GitHub en nuestro caso)

Los comandos `git add .` y `git commit -m "Good explanation of your file changes"` se utilizan para indexar y guardar los archivos en el repositorio de nuestro ordenador, y utilizaremos `git push` para enviar los cambios a GitHub. Esto es confuso cuando lo lees la primera vez, así que vamos a dibujar el flujo:

![](<.contenido/imagen (71).png>)

![](<.content/image (206).png>)

### ¿Qué problema resuelve Git?

Git es una herramienta de control de versiones, utilizada para mantener el historial de cambios, y facilitar la colaboración. Se utiliza para resolver muchos problemas, pero hoy vamos a centrarnos en cómo:

* Nos ayuda a compartir información.
* Permite a la gente hacer sus propios cambios en esa información, y compartirla de nuevo.
* Nos permite hacer puntos de control para que podamos guardar nuestro trabajo a medida que avanzamos.
* Nos permite hacer un seguimiento de cómo ha cambiado la información entre cada punto de control, y volver a versiones anteriores de nuestro trabajo si queremos ver lo que intentamos antes, o deshacer cambios.
* Nos permite probar más cosas, porque si no funcionan, siempre podemos volver a lo que teníamos funcionando antes, volviendo a un punto de control.

#### Versioning <a href="#versioning" id="versioning"></a>

Usamos Git para hacer un seguimiento de las diferentes versiones de los archivos.

Tal vez hayas tenido esta experiencia antes...

![](<.contenido/imagen (156).png>)

Es probable que en el pasado hayas guardado un documento en un archivo con el nombre "borrador", y luego otro con el nombre "versión 1", y finalmente uno llamado "final", y luego "realmente final", y luego "final tras comentarios". Puede ser difícil saber cuál es la última y seguir el orden de los archivos. Pero conservamos estos archivos porque son útiles y puede que queramos comprobar algo de ellos.

Git nos ayuda a evitar este problema. Antes de ver cómo nos ayuda Git, hagamos un ejercicio:

#### Ejercicio 1 (10 minutos) <a href="#ejercicio-1-10-minutos" id="ejercicio-1-10-minutos"></a>

Abre estos tres enlaces - son diferentes etapas de un borrador de entrada de blog sobre CodeYourFuture:

* [final](https://codeyourfuture.github.io/git-draft-blog-post-example/final)
* [revisado](https://codeyourfuture.github.io/git-draft-blog-post-example/revised)
* [v1](https://codeyourfuture.github.io/git-draft-blog-post-example/v1)

Intenta encontrar todas las diferencias entre estos tres documentos. ¿Puedes averiguar cuál es el documento final que se iba a publicar en el sitio web?

Probablemente te resulte difícil ver todas las diferencias (algunas son muy pequeñas, como añadir o quitar una coma) y no sea evidente cuál es la versión más completa.

### ¿Cómo ayuda Git? <a href="#cómo-ayuda-git" id="cómo-ayuda-git"></a>

Imagina que tu profesor quiere que todos los alumnos de la clase respondan a tres preguntas y envíen las respuestas. ¿Qué capacidades necesitaríamos para poder hacer eso?

**Primero**, el profesor necesita ser capaz de escribir las preguntas, y **almacenarlas** en algún lugar.

Cuando usamos Git, escribimos cosas en archivos dentro de una carpeta (pueden ser archivos de texto, documentos de Word, imágenes o cualquier tipo de archivo). Cuando guardamos estos archivos, decimos que los estamos _comprometiendo_, y llamamos a la carpeta donde los estamos guardando un _repositorio_ (o _repo_ para abreviar).

![](<.contenido/imagen (138).png>)

**A continuación**, el profesor debe colocar el repositorio en algún lugar donde los alumnos puedan acceder a él. A esto lo llamamos _pulsar_ el repositorio. El profesor no enviará una copia a cada alumno, sino que pondrá una copia en algún lugar de Internet, y les dirá a los alumnos dónde está. El lugar en el que los profesores de este curso harán el push es un sitio web llamado [GitHub](https://github.com/), pero hay otros sitios web a los que podrían hacer el push si quisieran. Esta es la diferencia entre Git y GitHub - Git es una forma de almacenar y compartir archivos, y GitHub es un sitio web donde se puede utilizar Git.

![](<.content/image (87).png>)

**Entonces**, ahora que el profesor ha empujado las preguntas, cada alumno necesita ser capaz de **obtener las preguntas en su ordenador**.

Cuando usamos Git, llamamos a esto _clonar_ el repositorio del profesor (porque estamos haciendo nuestra propia copia). Después de clonar el repositorio, tendremos en nuestro ordenador la misma carpeta que el profesor creó, confirmó y envió.

![](<.content/image (4).png>)

### The Git Cheatsheet <a href="#the-git-cheatsheet" id="the-git-cheatsheet"></a>

Tendemos a hacer las mismas cuatro o cinco cosas en Git una y otra vez, pero puede ser fácil olvidarlas. Hay una referencia práctica en [Git Guide](https://syllabus.migracode.org/git) y [Git CheatSheet](https://education.github.com/git-cheat-sheet-education.pdf) para ayudarte a recordar.

Repasemos juntos una de las secciones: "Quiero pasar código de un repositorio a mi ordenador (Clonación)". Tiene un video, para mostrarnos lo que debemos hacer, y explica cada paso en el texto.

Lo usaremos en nuestro próximo ejercicio:

#### Ejercicio 2 (15 minutos) <a href="#ejercicio-2-15-minutos" id="ejercicio-2-15-minutos"></a>

Los voluntarios de Code Your Future ya han empujado un repositorio de ejemplo, así que vas a intentar clonarlo desde GitHub a tu ordenador.

Intenta seguir las instrucciones etiquetadas como "Quiero obtener código de un repositorio en mi ordenador (Clonación)" de la [Git Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf). El repositorio que queremos clonar es `https://github.com/CodeYourFuture/cyf-demo-repo`.

Cuando hayas terminado el ejercicio, deberías tener `file.txt` abierto en VS Code.

### ¿Qué acabamos de hacer? <a href="#qué-acabamos-de-hacer" id="qué-acabamos-de-hacer"></a>

![](<.content/image (24).png>)

Cada uno de ustedes acaba de clonar un repositorio que CodeYourFuture creó en su ordenador, y abrió su copia de uno de los archivos. Este es el proceso que vais a seguir para conseguir vuestros deberes cada semana.

### Hagamos algunos deberes (demo guiada por el profesor) <a href="#lets-do-some-homework-teacher-led-demo" id="lets-do-some-homework-teacher-led-demo"></a>

El archivo que has abierto, `file.txt`, contiene una pregunta. Vamos a responder a la pregunta, y a enviarla como si fueran nuestros deberes.

Vamos a clonar nuestro repositorio en nuestro ordenador:

```
https://github.com/CodeYourFuture/cyf-demo-repo
```

Podemos editar el archivo en VS Code para responder a la pregunta, y guardarlo como de costumbre.

Después de guardar el archivo, si abrimos GitHub Desktop, algo interesante ha cambiado. A la izquierda, ahora dice "1 archivo cambiado", y a la derecha, nos muestra cuál ha sido el cambio. Las cosas que hemos eliminado tienen un fondo rojo, y las cosas que hemos añadido tienen un fondo verde.

(Si has cambiado una línea, la versión antigua aparecerá con fondo rojo, y la nueva versión con fondo verde).

![](<.contenido/imagen (131).png>)

Esta es una forma muy útil de revisar nuestros deberes antes de entregarlos. Si hemos borrado cosas accidentalmente, o cambiado cosas que no queríamos, podemos darnos cuenta ahora, y deshacerlas editando el archivo de nuevo.

Cuando estemos contentos con nuestro cambio, podemos pulsar el botón "Commit to main". Eso le dice a Git "Este cambio es un cambio interesante, quiero mantenerlo". No necesitas esperar hasta que tengas tus respuestas perfectas antes de confirmar, de hecho es mejor hacer muchas confirmaciones a medida que trabajas - ¡volveremos a esto en un momento!

Esto no copia nuestro cambio a ningún otro ordenador - no irá a GitHub - confirmar es algo que sólo hacemos en nuestro ordenador.

#### Ejercicio 3 (10 minutos) <a href="#ejercicio-3-10-minutos" id="ejercicio-3-10-minutos"></a>

Intenta hacer lo que acaba de hacer tu profesor:

1. Responde a la pregunta en `file.txt` en VS Code y guarda los cambios.
2. Mira el diff en el escritorio de GitHub - ¿se ve como esperabas?
3. 3. Haz un commit en tu repositorio local.

#### La demo guiada por el profesor continúa... <a href="#teacher-led-demo-continues" id="teacher-led-demo-continues"></a>

Ahora, debido a que hemos confirmado un cambio, nuestra copia del repositorio es diferente de la copia de CodeYourFuture. GitHub Desktop nos da ahora un nuevo botón: "Empujar origen" ("origen" es como Git llama a "desde dónde he clonado este repositorio"). Si lo pulsamos, intentará enviar nuestro cambio a la versión de CodeYourFuture.

Antes no teníamos este botón, porque aunque habíamos cambiado los archivos, no habíamos confirmado ningún cambio. Hay una distinción importante aquí: Cuando guardamos archivos en VS Code, los almacenamos en el archivo de nuestro ordenador, pero Git no los confirma automáticamente. Se da cuenta de los cambios (¡nos los ha mostrado!), y nos pregunta si queremos confirmarlos. Sólo después de que los hayamos confirmado nos permite enviarlos. Hablaremos de cuándo quieres confirmar más adelante.

Así que, estamos contentos con nuestra tarea, la hemos confirmado, ¡intentemos empujarla!

### Forking <a href="#forking" id="forking"></a>

GitHub Desktop acaba de darnos una advertencia realmente útil, ¡pero utiliza algunas palabras que aún no hemos visto!

Acabamos de intentar enviar nuestros cambios a la copia de CodeYourFuture de este repositorio. ¡Pero no se nos permite hacer eso! ¡Imagina que cualquiera pudiera subir lo que quisiera a nuestro repositorio! Alguien podría borrar accidentalmente todas las preguntas, o añadir las respuestas a todas las preguntas, ¡o convertir los deberes de HTML en un montón de preguntas sobre verduras!

Para evitar esto, usamos algo llamado _fork_ y algo llamado _pull request_.

¿Recuerdas que cuando clonamos el repositorio, pegamos `https://github.com/CodeYourFuture/cyf-demo-repo` como el lugar desde el que clonar? Echemos un vistazo a eso:

![](<.content/image (126).png>)

Esto está diciendo "En GitHub, el usuario `CodeYourFuture` tiene un repositorio llamado `cyf-demo-repo`, quiero eso".

GitHub también te permite alojar tu propia copia del repositorio en GitHub. Si tu nombre de usuario es `EagerLearner`, ¿puedes adivinar en qué URL estaría tu repositorio?

Así es, ¡https://github.com/EagerLearner/cyf-demo-repo!

![](<.content/image (50).png>)

Esto se llama un _fork_. Es una copia del repositorio, donde se te permite hacer cambios. Así que cuando GitHub Desktop nos acaba de preguntar "¿Quieres hacer un fork de este repositorio?", lo que realmente está diciendo es "No tienes permiso para hacer cambios en el repositorio de CodeYourFuture, ¿te gustaría hacer tu propia copia en GitHub donde _tienes_ permiso para hacer cambios, y poner tus cambios ahí?".

Eso suena exactamente a lo que queremos hacer, así que haremos clic en el botón "Fork This Repository".

Entonces GitHub nos pregunta si queremos hacer un fork "Para contribuir al proyecto padre" (es decir, porque queremos trabajar con CodeYourFuture) o "Para mis propios fines" (es decir, porque queremos hacer nuestras propias cosas aparte de CodeYourFuture). Nosotros queremos trabajar con CodeYourFuture, así que seleccionaremos "Para contribuir al proyecto padre" y pulsaremos Continuar.

Ahora si pulsamos "Push origin", copiará nuestros cambios a nuestro fork en GitHub.

![](<.content/image (60).png>)

Si te olvidas de esto, ¡está en la [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)! Echa un vistazo a la sección "Quiero enviar mi código a voluntarios (Pushing)".

### Hacer un Pull Request <a href="#making-a-pull-request" id="making-a-pull-request"></a>

Ahora que hemos empujado nuestra tarea a nuestro fork, ¡necesitamos informar a CodeYourFuture sobre ella, para que los voluntarios sepan que tienen que echarle un vistazo!

Hacemos esto con algo llamado _pull request_. Es un nombre un poco raro en el contexto de los deberes.

Normalmente, cuando la gente introduce cambios en una bifurcación de GitHub, lo hace porque quiere que la persona propietaria del repositorio vea los cambios y los incorpore a su repositorio. Por ejemplo, esta página web en la que estamos leyendo el temario ahora mismo está alojada en GitHub, y si alguien detecta un error tipográfico, puede corregirlo, subirlo a su fork y solicitar a CodeYourFuture que incorpore su cambio a la versión de CodeYourFuture (de ahí el nombre pull request, "solicitud de incorporación de cambios").

Llamamos "fusionar" el cambio de alguien en un repositorio, porque estamos fusionando lo que estamos introduciendo en nuestro repositorio con lo que teníamos antes.

Para enviar los deberes, cada semana vas a crear un pull request, y un voluntario lo mirará y te dará su opinión, pero no vamos a incluir tus deberes en la copia de CodeYourFuture (¡entonces el siguiente estudiante tendría las respuestas cuando intentara leer las preguntas!). Crearás pull requests, pero no incorporaremos tus cambios al repositorio.

En GitHub Desktop, si abres el menú Branch, y haces clic en "Create Pull Request", se abrirá tu navegador web en GitHub, y te mostrará los cambios para los que estás a punto de hacer un pull request. Este es otro buen momento para comprobar que estás contento con tu tarea (si no lo estás, vuelve a VS Code, haz tus cambios, confírmalos, envíalos a origen de nuevo, y actualiza esta página).

Si estás satisfecho, pulsa el botón "Create pull request". Rellena los detalles del formulario, para que los voluntarios sepan lo que van a revisar, y pulsa "Crear pull request".

Ahora ya hay una solicitud de extracción que los voluntarios pueden consultar. Pueden ver quién hizo el pull request, y ver todos los cambios que has hecho.

#### Ejercicio 4 (15 minutos) <a href="#ejercicio-4-15-minutos" id="ejercicio-4-15-minutos"></a>

¡Haz tú mismo un pull request con tu cambio!

1. Intenta empujar tus cambios, haz un fork y luego empuja realmente tus cambios.
2. Haz tu primer pull request.

Si te quedas atascado, echa un vistazo a la [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf) :)

#### Ejercicio 5 (5 minutos) <a href="#ejercicio-5-5-minutos" id="ejercicio-5-5-minutos"></a>

Hay otro fichero en el repositorio que has clonado, `otro-archivo.txt`.

1. Ábrelo
2. Responde a la pregunta que aparece en el archivo
3. Confirme
4. y Empujar

Observa que un par de cosas son diferentes esta vez.

No le pide que haga un fork del repositorio - eso es porque ya tiene un fork al que puede hacer push.

También puede notar que si hace clic en el elemento de menú "Crear Pull Request", le lleva a una página diferente. No tiene un botón "Crear Pull Request", tiene un botón "Ver Pull Request". Esto se debe a que si ya tiene una solicitud de extracción abierta, cuando introduzca más cambios, se actualizará su solicitud de extracción existente.

Esto es útil para responder a la retroalimentación que recibe en su tarea. Hay formas de abrir más de una pull request a la vez (usando algo llamado ramas), sobre las que aprenderemos en el futuro, pero por ahora, ¡una debería bastar!

### Getting feedback <a href="#getting-feedback" id="getting-feedback"></a>

Cuando hayas hecho tu pull request, nuestros voluntarios serán notificados. Ellos revisarán tus cambios. Cuando hayan terminado, recibirás un correo electrónico. Estas son algunas de las cosas que pueden hacer:

* Hacer comentarios con sugerencias, ya sea sobre un fragmento de código en particular, o sobre todo el pull request.
* Añadir etiquetas al pull request (por ejemplo, marcarlo como completo o inacabado).

Si te dan sugerencias, deberías intentar implementarlas y enviar un nuevo commit. Si estás confundido, luchando, o los encuentras poco claros, puedes responder al comentario con un comentario propio, o preguntar en Slack.

### Historia <a href="#historia" id="historia"></a>

Una característica útil de Git es cómo almacena tus commits. En GitHub Desktop, si abres la pestaña Historial, puedes ver una lista de cada commit que se ha hecho en el repositorio, con el más antiguo en la parte inferior y el más reciente en la parte superior.

Si haces clic en uno de los commits, verás los cambios que se han producido en él. Esto puede ser realmente útil para entender cómo evolucionó el repositorio hasta su aspecto actual. También puede ayudarnos a averiguar cuándo se introdujeron los errores.

Siempre puedes ver una versión antigua de un archivo mirando en el historial de Git, y si quieres recuperarla, sólo tienes que copiarla y pegarla desde la vista del historial en tu editor de texto.

#### Cuándo hacer commit, push y pull request <a href="#when-to-commit-push-and-make-a-pull-request" id="when-to-commit-push-and-make-a-pull-request"></a>.

Debes comprometerte a menudo Cada vez que creas que has hecho algo que quieras volver a mirar, deberías hacer un commit.

Digamos que has hecho un sitio web, y en general se ve bien, pero estabas pensando en añadir un poco de color, o una animación. Antes de hacerlo, haz un commit, porque si rompes algo del CSS intentando añadir una animación, siempre puedes deshacerlo.

O si quieres probar varios colores diferentes, haz un commit para cada color, y así podrás ver fácilmente qué colores has probado y compararlos.

**Demostración guiada por el profesor: Cambiar los colores**

Un voluntario hizo un pequeño sitio web, que podemos encontrar en [https://github.com/CodeYourFuture/SampleGitWebsite](https://github.com/CodeYourFuture/SampleGitWebsite)

Tenían varias combinaciones de colores diferentes entre las que intentaban elegir. Como hicieron commits para cada opción, podemos ver sus elecciones y probarlas.

Si no hubieran hecho todos esos commits, probablemente habrían olvidado al menos uno de los colores y ahora no podríamos verlos. Quizá habrían perdido el color perfecto. Afortunadamente, podemos mirar en el historial de git y ver cada paso a lo largo del camino.

Del mismo modo, no es necesario que hayas terminado todo antes de hacer push; de hecho, ¡puede ser mejor hacer muchos push! Si tu ordenador se estropea, o borras accidentalmente tus archivos, o quieres hacer los deberes en el ordenador de otra persona, siempre puedes recuperar todo lo que hayas enviado a GitHub. Así que haz commits a menudo, ¡y push a menudo!

Tampoco necesitas haber terminado todos tus deberes para hacer un pull request. Si has estado luchando con una pregunta, puedes hacer un pull request y pedir ayuda (¡incluso puedes enlazarlo en Slack! Ayudará a los voluntarios a ayudarte, porque podrán ver exactamente el código con el que estás teniendo problemas). O si has hecho la mayor parte de la tarea, pero tienes problemas con algunas preguntas, un voluntario puede ver lo que has hecho y ayudarte, ¡pero sólo si puede ver tu código!

Haz commit a menudo, push a menudo y haz pull requests pronto.

Puede que notes que todos tus commits tienen mensajes como "Actualizar archivo.txt", mientras que los anteriores a que empezaras a editar tenían mensajes diferentes.

Los mensajes de confirmación pueden ser muy útiles para entender lo que hizo un cambio sin tener que leerlo todo. Intentemos un ejercicio para ayudarnos a entender esto:

#### Ejercicio 6 (10 minutos) <a href="#ejercicio-6-10-minutos" id="ejercicio-6-10-minutos"></a>

1. Clona [https://github.com/CodeYourFuture/git-log-example](https://github.com/CodeYourFuture/git-log-example) (si has olvidado cómo, consulta la [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)
2. Lee el archivo `README.md`. Mira a ver si encuentras algún problema en el archivo.
3. 3. Revisa el historial en GitHub Desktop. A ver si puedes averiguar cuándo y por qué se introdujo el problema.
4. 4. Haz un pull request para solucionar el problema.

#### Ejercicio 7 (5 minutos) <a href="#ejercicio-7-5-minutos" id="ejercicio-7-5-minutos"></a>

¿Recuerdas que antes vimos tres entradas de blog? ¡En realidad están en un repositorio en GitHub! [https://github.com/CodeYourFuture/git-draft-blog-post-example](https://github.com/CodeYourFuture/git-draft-blog-post-example)

Clona el repositorio y echa un vistazo. ¿Puedes encontrar ahora todas las diferencias entre ellos? ¿Puedes decir cuál era la versión final? ¿Cuánto más fácil/difícil es esto que sin Git?

### Mensajes de confirmación <a href="#commit-messages" id="commit-messages"></a>

Si miras a través del historial del repositorio Git, puede que hayas sido capaz de ver dónde estaba el problema sólo por el mensaje de confirmación, sin tener que mirar los cambios que se hicieron realmente. Si los mensajes de confirmación fueran simplemente "Actualizar archivo.txt", ¡habría sido mucho más difícil!

Cuando hacemos confirmaciones en Git, intentamos dar mensajes claros y útiles, describiendo qué ha cambiado y por qué. (¡El por qué es realmente importante! Siempre puedes averiguar _qué_ ha cambiado leyendo el cambio en sí, pero es mucho más difícil averiguar _por qué_ si nadie lo ha escrito).

Hay una convención en el uso de Git para utilizar el siguiente formato para los mensajes de confirmación:

```
Resumen de una frase

Explicación más larga del cómo, las razones, excepciones, o cualquier cosa que pueda sorprender.
Puede constar de muchas frases y prolongarse durante mucho tiempo.
```

Intenta utilizar este formato cuando hagas tus propios commits. GitHub Desktop intenta fomentar esto teniendo dos cajas encima del botón "Commit to main" - una que es sólo una línea, y otra donde puedes poner muchas líneas.

![](<.content/image (82).png>)

Explicar _por qué_ estamos haciendo el cambio puede ayudar a la gente en el futuro a entender por qué las cosas se ven como se ven, y lo que es importante no cambiar.

### Glosario <a href="#glosario" id="glosario"></a>

Hemos introducido algunas cosas nuevas en esta clase, y puede ser un poco confuso saber cuál es cuál:

* **Git** es un sistema para almacenar cambios en archivos en commits, y compartirlos entre diferentes ordenadores. También hay otros sistemas que hacen esto, pero Git es el más popular.
* GitHub** es un sitio web que almacena una copia de tu repositorio Git y te permite clonarlo y enviarle cambios. También hay otros sitios web que pueden hacer esto, pero GitHub es el más popular.
* **GitHub Desktop** es un programa hecho por GitHub para permitirte usar Git fácilmente desde tu ordenador. Más adelante en el curso, también utilizaremos otros programas para usar Git.



### **Más Recursos**

* Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
* [¿Cómo funciona GitHub? (30min)](https://www.youtube.com/watch?v=E8TXME3bzNs)
* Sigue este tutorial para aprender los comandos básicos de Git [https://www.codeschool.com/courses/try-git](https://www.codeschool.com/courses/try-git)
* Otro buen recurso: Git - la guía sencilla [http://rogerdudler.github.io/git-guide/](http://rogerdudler.github.io/git-guide/)
* Un tutorial más detallado que profundiza en temas avanzados de Git - [https://www.atlassian.com/git/tutorials/what-is-version-control](https://www.atlassian.com/git/tutorials/what-is-version-control)
* También puedes consultar esta explicación visual de los diferentes comandos y lo que hacen: [http://ndpsoftware.com/git-cheatsheet.html#loc=workspace](http://ndpsoftware.com/git-cheatsheet.html#loc=workspace)
* Este Glosario tiene definiciones de los términos normalmente usados con Git: [https://help.github.com/articles/github-glossary/](https://help.github.com/articles/github-glossary/)

###
