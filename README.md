# 🚀 Guía Completa: Despliegue de React App en Firebase Hosting

Esta guía te lleva paso a paso para desplegar una aplicación React en Firebase Hosting.

## 📋 Prerrequisitos

- ✅ Node.js instalado
- ✅ Proyecto React creado y funcionando
- ✅ Cuenta de Google/Gmail
- ✅ Acceso a Firebase Console

---

## 🔧 Paso 1: Instalación de Firebase CLI

Instala Firebase Tools globalmente en tu sistema:

```bash
npm install -g firebase-tools
```

**Salida esperada:**
```
npm warn deprecated node-domexception@1.0.0: Use your platform's native DOMException instead
changed 715 packages in 38s
82 packages are looking for funding
  run `npm fund` for details
```

---

## 🔑 Paso 2: Autenticación con Firebase

Inicia sesión en tu cuenta de Google:

```bash
firebase login
```

**Si ya estás logueado verás:**
```
Already logged in as tu-email@gmail.com
```

**Si no estás logueado:**
- Se abrirá tu navegador
- Selecciona tu cuenta de Google
- Autoriza Firebase CLI

---

## 🏗️ Paso 3: Crear Proyecto en Firebase Console (Opcional)

Si no tienes un proyecto, créalo en [Firebase Console](https://console.firebase.google.com):

1. **Clic en "Agregar proyecto"**
2. **Nombre del proyecto:** `futravif-controler-estudent`
3. **Habilitar Google Analytics:** Opcional
4. **Crear proyecto**

---

## ⚙️ Paso 4: Inicializar Firebase en tu Proyecto React

En la terminal, navega a tu carpeta del proyecto React:

```bash
cd ruta/a/tu/proyecto-react
firebase init
```

### 4.1 Confirmar inicialización
```
? Are you ready to proceed? (Y/n)
```
**Respuesta:** `Y` + ENTER

### 4.2 Seleccionar características
```
? Which Firebase features do you want to set up for this directory?
❯◯ Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys
```

**Instrucciones:**
- Usa **flechas ↑↓** para navegar
- Presiona **ESPACIO** para seleccionar Hosting (◯ → ◉)
- Presiona **ENTER** para continuar

### 4.3 Seleccionar proyecto
```
? Please select an option:
❯ Use an existing project
  Create a new project
```

**Si tienes proyecto:** Selecciona "Use an existing project"
**Si no tienes proyecto:** Selecciona "Create a new project"

### 4.4 Configurar Hosting

#### Directorio público:
```bash
? What do you want to use as your public directory? (public)
```
**Respuesta:** `build` ⚠️ **MUY IMPORTANTE: Escribir "build", NO "public"**

#### Single Page Application:
```bash
? Configure as a single-page app (rewrite all urls to /index.html)? (Y/n)
```
**Respuesta:** `Y` + ENTER

#### GitHub Actions:
```bash
? Set up automatic builds and deploys with GitHub? (y/N)
```
**Respuesta:** `N` + ENTER

#### Sobrescribir index.html:
```bash
? File build/index.html already exists. Overwrite? (y/N)
```
**Respuesta:** `N` + ENTER

### 4.5 Configuración completa
```
✔ Firebase initialization complete!
```

---

## 🔨 Paso 5: Construir la Aplicación React

Genera los archivos optimizados para producción:

```bash
npm run build
```

**Salida esperada:**
```
> futravif-app@0.1.0 build
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:
  XX.XX KB  build/static/js/[hash].js
  X.XX KB   build/static/css/[hash].css

The build folder is ready to be deployed.
```

---

## 🚀 Paso 6: Desplegar a Firebase Hosting

Sube tu aplicación a Firebase:

```bash
firebase deploy
```

**Salida esperada:**
```
=== Deploying to 'futravif-controler-estudent'...

i  deploying hosting
i  hosting[futravif-controler-estudent]: beginning deploy...
i  hosting[futravif-controler-estudent]: found XX files in build
✔ hosting[futravif-controler-estudent]: file upload complete
i  hosting[futravif-controler-estudent]: finalizing version...
✔ hosting[futravif-controler-estudent]: version finalized
i  hosting[futravif-controler-estudent]: releasing new version...
✔ hosting[futravif-controler-estudent]: release complete

✔ Deploy complete!

Project Console: https://console.firebase.google.com/project/futravif-controler-estudent
Hosting URL: https://futravif-controler-estudent.web.app
```

---

## 🌐 Paso 7: Verificar Despliegue

**Tu aplicación estará disponible en:**
- **URL principal:** `https://tu-proyecto.web.app`
- **URL alternativa:** `https://tu-proyecto.firebaseapp.com`

**Verifica que:**
- ✅ La página carga correctamente
- ✅ Los estilos se aplican
- ✅ Las imágenes y recursos cargan
- ✅ La navegación funciona (para SPAs)

---

## 📁 Archivos Creados por Firebase

Después de la inicialización, encontrarás estos archivos:

### `firebase.json`
```json
{
  "hosting": {
    "public": "build",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

### `.firebaserc`
```json
{
  "projects": {
    "default": "tu-proyecto-id"
  }
}
```

---

## 🔄 Comandos para Actualizaciones Futuras

### Redesplegar cambios:
```bash
# 1. Construir nueva versión
npm run build

# 2. Desplegar
firebase deploy
```

### Solo desplegar hosting:
```bash
firebase deploy --only hosting
```

### Ver historial de despliegues:
```bash
firebase hosting:releases
```

---

## 🛠️ Comandos Útiles de Firebase CLI

```bash
# Ver proyectos disponibles
firebase projects:list

# Cambiar de proyecto
firebase use proyecto-id

# Ver información del proyecto actual
firebase use

# Previsualizar antes de desplegar
firebase serve

# Ver logs de funciones (si las usas)
firebase functions:log
```

---

## ⚠️ Solución de Problemas Comunes

### Error: "Public directory 'public' does not exist"
**Solución:** Asegúrate de usar `build` como directorio público, no `public`.

### Error: "No Firebase project directory detected"
**Solución:** Ejecuta `firebase init` en la carpeta raíz de tu proyecto React.

### Error: Página en blanco después del deploy
**Solución:** 
1. Verifica que ejecutaste `npm run build` antes de `firebase deploy`
2. Confirma que configuraste como SPA (rewrite rules)

### Error: 404 en rutas de React Router
**Solución:** Asegúrate de haber respondido "Y" a la pregunta sobre SPA.

---

## 📚 Recursos Adicionales

- [Documentación Firebase Hosting](https://firebase.google.com/docs/hosting)
- [Firebase CLI Reference](https://firebase.google.com/docs/cli)
- [React Deployment Guide](https://create-react-app.dev/docs/deployment/)

---

## 🎉 ¡Felicitaciones!

Tu aplicación React está ahora desplegada y accesible mundialmente a través de Firebase Hosting. 

**Recuerda:** Cada vez que hagas cambios en tu código, repite los pasos 5 y 6 para actualizar tu aplicación en producción.
