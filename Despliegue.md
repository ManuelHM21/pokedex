# Guía de Despliegue para la Aplicación PokeDex

Este documento describe el proceso para desplegar la aplicación PokeDex en la nube usando Vercel, incluyendo la configuración de seguridad necesaria.

## Prerrequisitos

- Cuenta en [Vercel](https://vercel.com)
- Repositorio de Git con el código de la aplicación
- Node.js y npm instalados localmente

## Pasos para el Despliegue

### 1. Preparación del Proyecto

Antes de desplegar, asegúrate de que tu aplicación esté correctamente configurada para producción:

```bash
# Instalar dependencias
npm install

# Compilar la aplicación para producción
npm run build
```

### 2. Configuración de Seguridad

Crea un archivo `vercel.json` en la raíz de tu proyecto para configurar los encabezados de seguridad:

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "Content-Security-Policy",
          "value": "default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com https://fonts.gstatic.com; font-src 'self' https://fonts.googleapis.com https://fonts.gstatic.com; img-src 'self' data: https://raw.githubusercontent.com; connect-src 'self' https://beta.pokeapi.co; frame-src 'self'"
        },
        {
          "key": "X-Frame-Options",
          "value": "SAMEORIGIN"
        },
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "Referrer-Policy",
          "value": "strict-origin-when-cross-origin"
        },
        {
          "key": "Permissions-Policy",
          "value": "camera=(), microphone=(), geolocation=(), interest-cohort=()"
        }
      ]
    }
  ]
}
```

Esta configuración proporciona protección contra varios tipos de ataques web comunes y permite el acceso a recursos externos necesarios como Google Fonts y la API de PokeAPI.

### 3. Despliegue en Vercel

#### Opción 1: Despliegue desde la Interfaz Web

1. Inicia sesión en [Vercel](https://vercel.com)
2. Haz clic en "New Project"
3. Importa tu repositorio de Git (GitHub, GitLab o Bitbucket)
4. Configura el proyecto:
   - Framework Preset: Angular
   - Build Command: `npm run build` (o el comando de construcción que uses)
   - Output Directory: `dist/[nombre-de-tu-proyecto]`
5. Haz clic en "Deploy"

#### Opción 2: Despliegue desde la Línea de Comandos

1. Instala la CLI de Vercel:
   ```bash
   npm install -g vercel
   ```

2. Inicia sesión en tu cuenta:
   ```bash
   vercel login
   ```

3. Despliega la aplicación:
   ```bash
   vercel
   ```

4. Sigue las instrucciones interactivas para configurar el proyecto.

### 4. Verificación del Despliegue

Una vez completado el despliegue, Vercel proporcionará una URL para acceder a tu aplicación (por ejemplo, `https://pokedex-username.vercel.app`).

Para verificar que todo funciona correctamente:

1. Abre la URL proporcionada en tu navegador
2. Comprueba que los datos de la API de PokeAPI se cargan correctamente
3. Verifica que los estilos y fuentes se están aplicando correctamente
4. Utiliza las herramientas de desarrollo del navegador para confirmar que no hay errores de seguridad

### 5. Configuración de Dominio Personalizado (Opcional)

Si deseas usar un dominio personalizado para tu aplicación:

1. En el dashboard de Vercel, selecciona tu proyecto
2. Ve a "Settings" > "Domains"
3. Agrega tu dominio personalizado
4. Sigue las instrucciones para configurar los registros DNS

## Solución de Problemas Comunes

### Errores de Política de Seguridad de Contenido (CSP)

Si ves errores relacionados con CSP en la consola del navegador, es posible que necesites ajustar las directivas en el archivo `vercel.json` para permitir recursos adicionales.

### Error 500 Internal Server Error

Si la aplicación muestra un error 500:

1. Verifica los logs de despliegue en el dashboard de Vercel
2. Comprueba la conexión con la API de PokeAPI
3. Asegúrate de que las directivas CSP permiten todas las conexiones necesarias

### Recursos No Cargados

Si algunos recursos no se cargan (imágenes, fuentes, etc.):

1. Verifica la configuración CSP para asegurarte de que los dominios de origen están permitidos
2. Comprueba las URLs de los recursos para asegurarte de que son correctas

## Mantenimiento y Actualizaciones

Para actualizar tu aplicación desplegada:

1. Realiza los cambios en tu código
2. Haz commit y push a tu repositorio
3. Vercel detectará automáticamente los cambios y desplegará la nueva versión

---

Con esta guía, deberías poder desplegar exitosamente tu aplicación PokeDex en Vercel con las configuraciones de seguridad apropiadas. Si tienes alguna pregunta o problema durante el proceso de despliegue, consulta la [documentación oficial de Vercel](https://vercel.com/docs) o ponte en contacto con el equipo de soporte.
