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


Pregunta 7 (2 pts). Ordene las etapas de validación que ejecuta el job frontend y explique por qué npm ci se ejecuta
antes que las pruebas.

Respuesta:
1: Obtener el codigo    actions/checkout@v4
2: Configurar node.js   actions/setup-node@v4
3: instalar dependencias    npm ci
4: Ejecutar las pruebas     npm test
5: Compilar el frontend con angular  npm run build

npm ci se debe ejecutar antes porque para ejecutar las pruebas primero se deben descargar las dependencias. Es como si intentaramos ejecutar un programa antes de tenerlo instalado, simplemente no tiene sentido.


PD: sin querer en los pasos anteriores le di a merge en el pull request, por lo que he tenido crear otro Pull request y dejarlo abierto. 


Pregunta 8 (3 pts). Después del push, indique qué etapa del pipeline falla y qué ocurre con las etapas siguientes

Respuesta: 
El fallo esta en el paso 4, es decir, al ejecutar las pruebas (npm test). La prueba esperaba encontrar "Titulo incorrecto" pero la pagina muestra "catalogo de recursos". Al fallar esto, se bloquea y se omiten los demas pasos


Pregunta 9 (3 pts). ¿Debería integrarse este Pull Request a main mientras el pipeline está fallando? Justifique

Respuesta:
No. Justamente es esto para lo que sirve el CI/CD. Si le damos a merge cuando el pipeline esta fallando, sabemos que en la rama main dara ese mismo error, y por lo tanto sabemos que caera nuestra Web en produccion



Pregunta 10 (4 pts). Clasifique cada elemento como “versionable”, “variable/configuración” o “secreto/no
versionable”: package.json, API_URL pública, AWS_REGION, DB_PASSWORD, API_TOKEN, terraform.tfstate.

Respuesta:
- package.json: Versionable. Es el archivo que define las dependencias del proyecto y los scripts para compilar, por lo que tiene que estar en el repositorio.
- API_URL pública: Variable/configuración. Es la URL de una API a la que se conecta la app. Depende de si estamos en pruebas o producción, pero al ser pública no tiene datos sensibles.
- AWS_REGION: Variable/configuración. Solo indica la región de los servidores (como us-east-1), es configuración y no un secreto.
- DB_PASSWORD: Secreto/no versionable. Es la contraseña de la base de datos, si se sube a git cualquiera podría acceder o borrar la información.
- API_TOKEN: Secreto/no versionable. Es un token privado de autenticación con permisos, nunca debe subirse al repositorio.
- terraform.tfstate: Secreto/no versionable. Contiene toda la información de la infraestructura y muchas veces guarda contraseñas y datos sensibles en texto plano.


Pregunta 11 (2 pts). ¿Por qué una contraseña o token no debe escribirse directamente dentro de ci.yml, cd.yml o un
archivo TypeScript del frontend?
Porque las contraseñas o tokens deben ser privadas, y si lo metemos dentro de esos archivos, cualquiera que pueda ver el repositorio pondra ver esas contraseñas, y esa informacion lo podra utilizar en nuestra contra. Si lo ponemos en el .gitignore nos aseguramos que solamente vamos a tener esa informacion de manera local. 

Pregunta 12 (2 pts). Si un secreto real fue incluido en un commit y luego se agrega su archivo a .gitignore, ¿queda
solucionado el problema? Explique qué acción adicional debe realizarse
No. Ese secreto ya queda visible en el historial de github. La solucion es quitar ese secreto y crear otro completamente nuevo, para que el anterior secreto se quede inservible.


Pregunta 13 (2 pts). ¿Qué diferencia existe entre terraform validate, terraform plan y terraform apply?

Respuesta:
- terraform validate: Solo revisa que el codigo y la sintaxis de los archivos de terraform esten bien escritos y no tengan fallos. No se conecta a ningun sitio ni crea nada.
- terraform plan: Es como una simulacion. Compara lo que hemos escrito con lo que hay actualmente y nos muestra que recursos se van a crear, cambiar o borrar, pero sin hacer ningun cambio real todavia.
- terraform apply: Es el comando que de verdad ejecuta las cosas y crea o modifica los recursos en la infraestructura real, guardando el estado en el archivo terraform.tfstate.


Pregunta 14 (2 pts). ¿Por qué ci.yml se activa con pull_request y cd.yml se activa con push sobre main?


Respuesta:
ci.yml sirve para probar y revisar el codigo de forma peventiva antes de mezclarlo a la rama main, evitando que entren errores o cosas rotas. En cambio, cd.yml es para desplegar, se activa cuando el codigo ya fue aprobado e integrado en main, lo que significa que ya esta probado y listo para enviarse al entorno de staging.


Pregunta 15 (2 pts). ¿Qué función cumple Terraform dentro de este flujo de CD?


Respuesta:
Cumple la funcion de automatizar el despliegue del frontend como infraestructura. En este caso particular, se encarga de limpiar el entorno anterior, crear la carpeta de staging y copiar de forma automatica todos los archivos que compilo angular.


Pregunta 16 (2 pts). ¿Por qué el workflow usa ${{ secrets.DEMO_TOKEN }} en lugar de escribir el valor directamente?

Respuesta:
Porque con GitHub Secrets el valor se guarda encriptado y no puede ver nadie. Si pusieramos la clave directamente en el archivo yml, quedaria en texto plano y cualquier persona con acceso al repositorio la podria ver. Es muy parecido a lo que ocurre en la pregunta 11.