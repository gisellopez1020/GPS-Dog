# 🐕 GPS-Dog (PetTracker)

Una aplicación web moderna para el rastreo GPS en tiempo real de mascotas, construida con React, Firebase y Leaflet.

## 📋 Descripción

PetTracker es una aplicación completa que permite a los dueños de mascotas monitorear y rastrear la ubicación de sus compañeros en tiempo real.

**⚠️ IMPORTANTE:** Esta es la aplicación web de visualización. Las ubicaciones GPS se capturan desde nuestra **[aplicación móvil en React Native Expo](https://github.com/gisellopez1020/App_Paw_Tracker)**, la cual obtiene las coordenadas GPS del dispositivo móvil y las envía a Firebase Realtime Database. Esta aplicación web consume esos datos para mostrar la ubicación en mapas interactivos.

### Arquitectura del Sistema

```
📱 App Móvil (React Native Expo)
    ↓ Captura GPS (latitud/longitud)
    ↓ Envía datos
☁️ Firebase Realtime Database
    ↓ Sincronización en tiempo real
💻 App Web (React + Vite) - Este repositorio
    ↓ Visualiza en mapas
🗺️ Leaflet Maps
```

La aplicación ofrece seguimiento GPS, historial de recorridos, visualización de mapas interactivos y consejos útiles para el cuidado de mascotas.

## ✨ Características

### Funcionalidades Web (Este Repositorio)

- 🔐 **Autenticación de usuarios** - Sistema completo de registro e inicio de sesión con Firebase
- 🗺️ **Mapas interactivos** - Visualización de ubicación en tiempo real usando Leaflet
- 📊 **Historial de recorridos** - Registro detallado de todas las ubicaciones visitadas
- 🔍 **Filtros de búsqueda** - Filtra recorridos por fecha y ubicación
- 👤 **Perfil de usuario** - Gestión de información personal
- 💡 **Tips y consejos** - Recomendaciones para el cuidado de mascotas
- 📱 **Diseño responsive** - Interfaz adaptable a diferentes dispositivos
- 🔄 **Sincronización en tiempo real** - Recibe actualizaciones instantáneas desde la app móvil

### Funcionalidades Móviles ([App Móvil](https://github.com/gisellopez1020/App_Paw_Tracker))

- 📍 **Captura de GPS** - Obtiene coordenadas en tiempo real del dispositivo móvil
- ⬆️ **Envío automático** - Transmite ubicaciones a Firebase automáticamente
- 🔋 **Rastreo continuo** - Seguimiento en segundo plano de la ubicación de tu mascota
- 📲 **App nativa** - Aplicación móvil desarrollada con React Native Expo

## 🛠️ Tecnologías

### Frontend

- **React 18.3** - Biblioteca principal de UI
- **Vite 5.4** - Herramienta de build y desarrollo
- **React Router DOM 6.27** - Navegación entre páginas
- **Bootstrap 5.3** - Framework CSS para estilos

### Mapas y Visualización

- **Leaflet 1.9** - Biblioteca de mapas interactivos
- **React Leaflet 4.2** - Integración de Leaflet con React
- **Recharts 2.13** - Gráficos y visualización de datos

### Backend y Base de Datos

- **Firebase 11.0** - Autenticación y base de datos en tiempo real
- **Firebase Realtime Database** - Almacenamiento de ubicaciones

### Utilidades

- **date-fns 4.1** - Manipulación y formateo de fechas
- **Lucide React 0.453** - Iconos modernos
- **ESLint** - Linting y calidad de código

## 📁 Estructura del Proyecto

```
GPS-Dog/
├── public/              # Archivos estáticos
├── src/
│   ├── assets/         # Imágenes y recursos
│   ├── components/     # Componentes reutilizables
│   │   ├── DynamicMap.jsx
│   │   ├── Layout.jsx
│   │   ├── LocationTracker.jsx
│   │   ├── MapComponent.jsx
│   │   └── Sidebar.jsx
│   ├── context/        # Context API de React
│   │   └── AuthContext.jsx
│   ├── pages/          # Páginas de la aplicación
│   │   ├── Home.jsx
│   │   ├── Index.jsx
│   │   ├── Login.jsx
│   │   ├── SignUp.jsx
│   │   ├── Map.jsx
│   │   ├── Perfil.jsx
│   │   ├── Tips.jsx
│   │   └── HistorialRecorridos.jsx
│   ├── styles/         # Archivos CSS
│   ├── App.jsx         # Componente principal
│   ├── main.jsx        # Punto de entrada
│   └── credenciales.js # Configuración de Firebase
├── package.json
└── vite.config.js
```

## 🚀 Instalación y Configuración

### Prerequisitos

- Node.js 16 o superior
- npm o yarn
- Cuenta de Firebase
- **[Aplicación móvil PawTracker](https://github.com/gisellopez1020/App_Paw_Tracker)** instalada en un dispositivo móvil (para captura de ubicaciones GPS)

### Pasos de instalación

1. **Clona el repositorio**

   ```bash
   git clone https://github.com/gisellopez1020/GPS-Dog.git
   cd GPS-Dog
   ```

2. **Instala las dependencias**

   ```bash
   npm install
   ```

3. **Configura Firebase**

   Crea un archivo `src/credenciales.js` con tu configuración de Firebase:

   ```javascript
   import { initializeApp } from "firebase/app";
   import { getAuth } from "firebase/auth";
   import { getDatabase } from "firebase/database";

   const firebaseConfig = {
     apiKey: "TU_API_KEY",
     authDomain: "TU_AUTH_DOMAIN",
     databaseURL: "TU_DATABASE_URL",
     projectId: "TU_PROJECT_ID",
     storageBucket: "TU_STORAGE_BUCKET",
     messagingSenderId: "TU_MESSAGING_SENDER_ID",
     appId: "TU_APP_ID",
   };

   export const appFirebase = initializeApp(firebaseConfig);
   export const auth = getAuth(appFirebase);
   export const database = getDatabase(appFirebase);
   ```

4. **Inicia el servidor de desarrollo**

   ```bash
   npm run dev
   ```

5. **Abre la aplicación**

   Navega a `http://localhost:5173` en tu navegador

## 📝 Scripts Disponibles

```bash
npm run dev      # Inicia el servidor de desarrollo
npm run build    # Construye la aplicación para producción
npm run preview  # Previsualiza la versión de producción
npm run lint     # Ejecuta el linter
```

## 🔧 Configuración de Firebase

### Configurar Realtime Database

1. Ve a tu consola de Firebase
2. Crea un proyecto nuevo o selecciona uno existente
3. Habilita **Realtime Database**
4. Configura las reglas de seguridad:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
```

### Habilitar Authentication

1. En la consola de Firebase, ve a **Authentication**
2. Habilita el método de autenticación **Email/Password**

## 🎯 Funcionalidades Principales

### 1. Autenticación

- Registro de nuevos usuarios
- Inicio de sesión
- Cierre de sesión automático al cerrar la pestaña
- Protección de rutas

### 2. Rastreo en Tiempo Real

- **Captura de ubicación:** La [aplicación móvil](https://github.com/gisellopez1020/App_Paw_Tracker) obtiene coordenadas GPS del dispositivo
- **Transmisión:** Las coordenadas se envían automáticamente a Firebase Realtime Database
- **Visualización:** Esta aplicación web recibe y muestra las ubicaciones en el mapa en tiempo real
- **Sincronización:** Actualización instantánea del mapa cuando se reciben nuevas coordenadas

### 3. Historial de Recorridos

- Visualización de todas las ubicaciones guardadas
- Filtrado por fecha y ubicación
- Edición de registros
- Vista detallada de cada recorrido

### 4. Visualización de Mapas

- Mapa interactivo con Leaflet
- Marcadores de ubicaciones
- Zoom y navegación

## 🌐 Navegación

- `/` - Página de inicio (Index)
- `/login` - Inicio de sesión
- `/signup` - Registro de usuario
- `/home` - Dashboard principal
- `/map` - Mapa en tiempo real
- `/perfil` - Perfil de usuario
- `/historial` - Historial de recorridos
- `/tips` - Tips y consejos

## 🔒 Seguridad

- Autenticación mediante Firebase Auth
- Sesiones protegidas con sessionStorage
- Rutas protegidas que requieren autenticación
- Cierre de sesión automático al cerrar el navegador

## 🔗 Proyectos Relacionados

- **[App Móvil PawTracker](https://github.com/gisellopez1020/App_Paw_Tracker)** - Aplicación móvil en React Native Expo para captura de ubicaciones GPS

## 📄 Licencia

Este proyecto está bajo la Licencia MIT.

## 👨‍💻 Autores

**Gisel Lopez**

- GitHub: [@gisellopez1020](https://github.com/gisellopez1020)

**Mónica Chicangana**

- GitHub: [@Monica0317](https://github.com/Monica0317)

**Maira Peña**

- GitHub: [@MairaPena](https://github.com/MairaPena)

## 📧 Contacto

Para preguntas o sugerencias, no dudes en contactar.

---

⭐ Si este proyecto te fue útil, dale una estrella en GitHub
