Respuestas del Laboratorio

Pregunta 1 (2 pts). ¿Por qué no se recomienda desarrollar directamente sobre main en este laboratorio?

Respuesta: La rama main se suele utilizar cuando el codigo esta listo para la produccion. Si el push que hago a la rama main esta mal y crashea el programa, se puede caer toda la web de la produccion. Si lo subo en otra rama, solamente la web de pruebas se vera afectada.


Pregunta 2 (2 pts). ¿Qué problema se evita al utilizar --skip-git al crear el proyecto Angular?

Respuesta:
Por defecto angular ya crea un repositorio git. Como nosotros ya hemos creado un proyecto de git manualmente, no tiene sentido crear otro repositorio dentro del repositorio que hemos creado. Con el comando de --skip-git, ignoramos que cree este segundo repositorio.


Pregunta 3 (2 pts). ¿Qué verifica npm run build en esta etapa del laboratorio?

Respuesta: 
el comando sirve para saber si todo se ha compilado correctamente. Esto es, por una parte sirve para identificar los errores de codigo y sintaxis. Por otra parte asegura que el proyecto se pueda construir con exito de manera local antes de pasar al CI/CD