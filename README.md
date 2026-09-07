Respuestas del Laboratorio

Pregunta 1 (2 pts). ¿Por qué no se recomienda desarrollar directamente sobre main en este laboratorio?

Respuesta: La rama main se suele utilizar cuando el codigo esta listo para la produccion. Si el push que hago a la rama main esta mal y crashea el programa, se puede caer toda la web de la produccion. Si lo subo en otra rama, solamente la web de pruebas se vera afectada.


Pregunta 2 (2 pts). ¿Qué problema se evita al utilizar --skip-git al crear el proyecto Angular?

Respuesta:
Por defecto angular ya crea un repositorio git. Como nosotros ya hemos creado un proyecto de git manualmente, no tiene sentido crear otro repositorio dentro del repositorio que hemos creado. Con el comando de --skip-git, ignoramos que cree este segundo repositorio.


Pregunta 3 (2 pts). ¿Qué verifica npm run build en esta etapa del laboratorio?

Respuesta: 
el comando sirve para saber si todo se ha compilado correctamente. Esto es, por una parte sirve para identificar los errores de codigo y sintaxis. Por otra parte asegura que el proyecto se pueda construir con exito de manera local antes de pasar al CI/CD


Pregunta 4 (2 pts). ¿Qué utilidad tiene revisar git status o git diff --cached antes de realizar un commit?

Respuesta:
git status sirve para ver que archivos se han cambiado desde el ultimo commit. Por otro lado, git diff --cached sirve para ver los cambios exactos (linea por linea) que van a entrar en el commit. Estos dos comandos son muy utiles para verificar que cambios hemos hecho y no subir librerias pesadas o archivos basura (como node_modules pro ejemplo)

Pregunta 5 (2 pts). ¿Qué evento activa el workflow ci.yml?

Respuesta:
Se activa cuando hacemos un pull request a la rama main. Es decir, si hacemos un push corriente a la rama main o a la rama de development, no se va a ejecutar nada. Pero si una vez hecho el push a la rama de development, hacemos un pull request a la rama main, entonces si se ejecuta el workflow. 

Pregunta 6 (2 pts). En runs-on: ubuntu-latest, ¿qué representa ubuntu-latest?

Respuesta: 
Significa en que entorno o sistema operativo se van a compilar y hacer esas pruebas. En este caso, se va a hacer en la distribucion ubuntu de linux. 
PD:al estar ejecutando yo de manera local en windows, cuando hacia el pull request, al ejecutar las pruebas daba un error. He averigado que era por temas de configuracion de package.json, por lo que he tenido que modificar este archivo. 

Pregunta 7 (2 pts). Ordene las etapas de validación que ejecuta el job frontend y explique por qué npm ci se ejecuta
antes que las pruebas.

Respuesta:
1: Obtener el codigo    actions/checkout@v4
2: Configurar node.js   actions/setup-node@v4
3: instalar dependencias    npm ci
4: Ejecutar las pruebas     npm test
5: Compilar el frontend con angular  npm run build

npm ci se debe ejecutar antes porque para ejecutar las pruebas primero se deben descargar las dependencias. Es como si intentaramos ejecutar un programa antes de tenerlo instalado, simplemente no tiene sentido.


