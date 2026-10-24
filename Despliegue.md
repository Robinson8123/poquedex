
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

## 3. Evidencia de Escaneo de Seguridad
Se auditó la URL pública en [SecurityHeaders.com](https://securityheaders.com/?q=https%3A%2F%2Fpokedex-cwcjg2ctgab9dja2.brazilsouth-01.azurewebsites.net%2F&followRedirects=on) obteniendo calificación **A+**
