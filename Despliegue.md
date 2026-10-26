
#  Despliegue y Configuración de Seguridad - PokéDex

## 1. Proceso de Despliegue en Azure App Service 

1. Se creó el recurso **App Service** en Azure con el sistema operativo **Windows** y el grupo de recursos `rg-proyecto-rs`
2. Se vinculó el **Centro de Implementación** con el repositorio de GitHub `https://github.com/Robinson8123/poquedex.git`
3. Se desplegó la aplicación Angular haciendo uso del archivo de configuración `web.config` para IIS

## 2. Configuración de Encabezados HTTP de Seguridad

Se incluyó el archivo `src/web.config` para asegurar la aplicación con calificación A+ en SecurityHeaders:

- `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`
- `X-Frame-Options: DENY`
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Permissions-Policy: geolocation=(), microphone=(), camera=()`
- `Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com data:; img-src 'self' data: https://raw.githubusercontent.com https://pokeapi.co; connect-src 'self' https://pokeapi.co;`


## 3: Integración Continua (GitHub Actions)
​Para automatizar el despliegue cada vez que se sube código al repositorio:

​Navegué hacia el recurso Web App recién creado.
​En el menú lateral izquierdo, bajo la sección Implementación, seleccioné Centro de implementación (Deployment Center).

​En Origen (Source), seleccioné GitHub.
​Autoricé la conexión de Azure con mi cuenta de GitHub.

​Seleccioné mi Organización, el Repositorio (pokedex) y la Rama (main).

​Al hacer clic en Guardar, Azure generó y configuró automáticamente un archivo de flujo de trabajo YAML (main_pokedex.yml) dentro de la carpeta .github/workflows/ en mi repositorio.

## 4.​En el archivo angular.json, registré el src/web.config en la sección de assets para asegurar que formara parte del build de producción.




## 5: Despliegue Final a Producción

Realicé un commit de todos los cambios de rutas relativas y seguridad en la terminal de mi entorno local:

git add .
git commit -m "feat: Configuración de seguridad web.config "
git push origin main

El push detonó automáticamente el Workflow de GitHub Actions.

Desde la pestaña Actions en GitHub, monitoreé el progreso de "Build and Deploy".

Al finalizar exitosamente, abrí la URL pública generada por Azure (https://pokedex-cwcjg2ctgab9dja2.brazilsouth-01.azurewebsites.net/) y verifiqué la carga correcta de imágenes de Pokémon y la seguridad mediante securityheaders.com.

## 6. Evidencia de Escaneo de Seguridad
Se auditó la URL pública en [SecurityHeaders.com](https://securityheaders.com/?q=https%3A%2F%2Fpokedex-cwcjg2ctgab9dja2.brazilsouth-01.azurewebsites.net%2F&followRedirects=on) obteniendo calificación **A**