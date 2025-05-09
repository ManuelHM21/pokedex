# Guía para Crear una Cuenta y Configurar el Entorno en la Nube (Vercel)

Este documento proporciona una guía detallada para crear una cuenta en la nube pública **Vercel**, así como las diferentes formas de autenticación disponibles y la configuración inicial para desplegar aplicaciones como PokeDex.

---

## 🔐 1. Métodos para Crear una Cuenta en Vercel

Puedes crear una cuenta en Vercel de tres formas distintas, según el proveedor Git que uses.

### ✅ Opción A: Usando GitHub (Recomendada)

1. Ve a [https://vercel.com](https://vercel.com)
2. Haz clic en **"Start with GitHub"**
3. Inicia sesión con tu cuenta de GitHub si no lo has hecho aún
4. Autoriza a Vercel a acceder a tus repositorios (puedes limitar el acceso)
5. Se creará tu cuenta de Vercel con acceso directo a tus proyectos de GitHub

### 🔄 Opción B: Usando GitLab

1. En la página principal de Vercel, selecciona **"Continue with GitLab"**
2. Serás redirigido para autorizar a Vercel a conectar con GitLab
3. Elige los repositorios que deseas importar y autoriza la integración

### ☁️ Opción C: Usando Bitbucket

1. Haz clic en **"Continue with Bitbucket"**
2. Autentica tu cuenta y acepta los permisos necesarios
3. Vercel mostrará tus repositorios disponibles para importar

> 📌 **Nota**: No se puede crear una cuenta solo con correo electrónico; Vercel requiere integración con un proveedor Git.

---

## ⚙️ 2. Configuración Inicial del Proyecto

Una vez creada tu cuenta, puedes empezar a desplegar tu aplicación:

### 1. Inicia Sesión y Crea un Proyecto

- Desde el panel de Vercel, haz clic en **"New Project"**
- Se mostrará la lista de repositorios de tu cuenta Git
- Elige el repositorio que contiene tu proyecto (por ejemplo: PokeDex)

### 2. Configura el Framework y Comandos

- Framework Preset: selecciona el que usas (React, Angular, Next.js, etc.)
- Build Command: por lo general es `npm run build`
- Output Directory: puede ser `build/`, `dist/` o `out/` según el framework

### 3. Despliega

- Haz clic en **"Deploy"** para iniciar el proceso de construcción y publicación

---

## ✅ 3. Recomendaciones Adicionales

- Usa variables de entorno si tu aplicación se comunica con APIs externas (`Settings > Environment Variables`)
- Mantén actualizado el repositorio de Git, ya que Vercel hace **despliegue continuo** con cada `git push`
- Considera usar un dominio personalizado si deseas profesionalizar tu URL

---

Con esta guía, tu cuenta en Vercel estará lista y conectada a tu repositorio Git para un flujo de trabajo moderno, rápido y seguro.