# Guía de Despliegue para la Aplicación PokeDex

Este documento describe el proceso para desplegar la aplicación PokeDex en la nube usando Vercel, incluyendo la configuración de seguridad necesaria.

<p align="center">
  <img src="/diagrama.png" alt="Arquitectura de la app" width="900"/>
</p>

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

### 3. Despliegue en Vercel

#### Opción 1: Interfaz Web

1. Inicia sesión en [Vercel](https://vercel.com)
2. Haz clic en "New Project"
3. Importa tu repositorio
4. Configura:
   - Framework Preset: Angular
   - Build Command: `npm run build`
5. Haz clic en "Deploy"

#### Opción 2: Línea de Comandos

```bash
# Instalar CLI
npm install -g vercel

# Iniciar sesión
vercel login

# Desplegar aplicación
vercel
```

### 4. Verificación del Despliegue

- Abre la URL proporcionada por Vercel
- Verifica carga de datos desde la API
- Asegúrate que no haya errores de seguridad

### 5. Dominio Personalizado (Opcional)

1. Ve a "Settings" > "Domains"
2. Agrega tu dominio personalizado
3. Configura los registros DNS según las instrucciones

### 6. Problemas Comunes

#### CSP

Ajusta el archivo `vercel.json` si ves errores en consola.

#### Error 500

- Revisa logs en Vercel
- Verifica conexión con la API

#### Recursos No Cargados

- Verifica configuración CSP
- Revisa las URLs de los recursos

### 7. Actualizaciones

1. Haz cambios en tu código
2. Haz `git push`
3. Vercel desplegará automáticamente los cambios

---

#### ¿Qué significa cada encabezado de seguridad y por qué se usa?

- **Content-Security-Policy (CSP)**: Define qué fuentes de contenido son válidas. Previene ataques como XSS (Cross Site Scripting) al restringir desde dónde se pueden cargar scripts, estilos, imágenes, etc.

- **X-Frame-Options**: Indica si el contenido de tu sitio puede ser mostrado dentro de un `<iframe>`. La opción `"SAMEORIGIN"` evita ataques de clickjacking al permitir sólo a tu mismo dominio embeber la página.

- **X-Content-Type-Options**: Evita que los navegadores intenten adivinar el tipo de contenido (MIME sniffing), lo cual puede abrir puertas a ataques. `"nosniff"` es la configuración recomendada.

- **Referrer-Policy**: Controla cuánta información del encabezado `Referer` se envía al navegar entre sitios. `"strict-origin-when-cross-origin"` protege la privacidad del usuario al no enviar información sensible del origen completo.

- **Permissions-Policy**: Especifica qué APIs del navegador están disponibles para el sitio. En este caso, se bloquea el acceso a cámara, micrófono, geolocalización y seguimiento por cohortes.

Estos encabezados refuerzan la seguridad de la aplicación protegiendo contra ataques comunes del lado del cliente y mejorando la privacidad del usuario.
