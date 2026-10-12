# Instrucciones de Copilot para este repositorio

Este repositorio es un conjunto de ejercicios de HTML para GitHub Classroom. La intención del proyecto es que el estudiante complete páginas HTML siguiendo instrucciones en [ejercicios/](../ejercicios/) y que las pruebas de Jest validen tanto la estructura del proyecto como el DOM resultante. La referencia principal es [README.md](../README.md).

## Comandos de instalación, pruebas y validación

- Instalación inicial:
  - `npm install`
- Ejecutar la suite completa:
  - `npm test`
- Ejecutar un archivo de prueba concreto (recomendado para depurar un ejercicio):
  - `npx jest tests/ejercicio/5-rutas-imagenes.test.js --runInBand`
  - `npx jest --runTestsByPath tests/ejercicio/5-rutas-imagenes.test.js`

No hay `lint` ni `build` definidos en [package.json](../package.json); la validación real del proyecto es únicamente Jest. El script de `npm test` ejecuta `jest` tal como está en [package.json](../package.json).

## Arquitectura general del repositorio

### Patrón de cada ejercicio
Cada ejercicio sigue este flujo:

1. Se describe la tarea en `ejercicios/ejercicio-N-*.md`.
2. El estudiante crea el resultado en `src/` (por ejemplo, carpetas o páginas HTML dentro de `src/ejercicio-1/`).
3. Las pruebas en `tests/ejercicio/*.test.js` verifican:
   - que existan las carpetas requeridas,
   - que el archivo HTML tenga la estructura mínima (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>` y `<title>`),
   - que el DOM contenga elementos HTML esperados (`img`, `h1`, `p`, etc.),
   - y que las rutas relativas o atributos como `alt` sigan las reglas del ejercicio.

Esto es un repositorio de contenido estático; no hay backend ni framework. La complejidad real está en la estructura de archivos del estudiante y en la validación DOM con JSDOM.

### Directorios clave

- [README.md](../README.md): explica el propósito del curso y cómo ver los ejercicios en Live Server.
- [ejercicios/](../ejercicios/): instrucciones en español de cada tarea.
- [src/](../src/): trabajo del estudiante; aquí se crean carpetas, archivos HTML y recursos como imágenes.
- [tests/](../tests/): pruebas automáticas; no deben modificarse para la resolución de ejercicios.
- [.github/workflows/](./workflows/): automatización de GitHub Classroom/autograding; también es parte del entorno del curso.

## Convenciones y patrones específicos del proyecto

### Trabajo permitido y no permitido

- El trabajo del estudiante se hace principalmente en `src/`.
- Se espera que no se editen archivos de pruebas ni configuraciones del proyecto: `tests/`, `.github/workflows/`, `package.json`, `jest.config.js`.
- En este repositorio, los ejercicios se basan en archivos HTML estáticos y carpetas de recursos. No se usa un stack de frontend moderno.

### Nomenclatura esperada

- Los archivos de ejercicios usan nombres en español: por ejemplo `ejercicio-1-crear-carpetas.md` y `ejercicio-5-rutas-imagenes.md`.
- El patrón de salida frecuente es `src/ejercicio-N/...` con archivos como `galeria.html` o estructurales del ejercicio.
- Se esperan subcarpetas como `images/`, `css/` o `js/` dependiendo del ejercicio, y las pruebas validan su existencia.

### Requisitos HTML básicos que se repiten

La base de muchos ejercicios es una página HTML mínima como esta:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <title>Ejemplo</title>
  </head>
  <body>
    <!-- contenido -->
  </body>
</html>
```

Las pruebas no solo comprueban que exista esta estructura, sino que además inspeccionan elementos concretos del DOM (por ejemplo `h1`, `p`, `img`, `alt`, rutas relativas, etc.), según cada ejercicio.

### Validación de pruebas

Algunas pruebas validan rutas relativas sin utilizar rutas absolutas del sistema y exigen atributos de accesibilidad como `alt`. Por ejemplo, los tests para imágenes revisan:

- existencia de la carpeta de imágenes,
- presencia de `img` en el HTML,
- que cada imagen tenga `alt`,
- y que la ruta de la imagen sea relativa y segura (`./`, `images/...`, etc.).

Las pruebas usan `fs` y `JSDOM`, y suelen realizar comprobaciones de archivo + DOM en lugar de depender únicamente de una sola capa.

## Consideraciones para futuras sesiones de Copilot

- Prioriza cambios en archivos de `src/` y en los archivos de ejercicio Markdown cuando sea necesario.
- Cuando generes contenido HTML para este repositorio, sigue la lógica educativa del curso: estructura semántica básica, rutas relativas y español.
- Al solucionar un ejercicio, verifica contra la prueba más cercana al ejercicio afectado en lugar de ejecutar la suite completa si no es necesario.
- Si necesitas crear o ajustar un ejercicio nuevo, mantén la misma convención del proyecto: instrucciones en `ejercicios/`, salida en `src/`, y pruebas en `tests/ejercicio/`.

## Referencias útiles

- [README.md](../README.md)
- [package.json](../package.json)
- [tests/test-runner.js](../tests/test-runner.js)
- [ejercicios/](../ejercicios/)
