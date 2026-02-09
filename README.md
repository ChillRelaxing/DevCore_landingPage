# 🚀 Guía de Instalación del Proyecto

¡Bienvenido al equipo! Sigue estos pasos para configurar el proyecto en tu máquina local desde cero.

## 📋 Requisitos Previos

Asegúrate de tener instalado lo siguiente:
- [Node.js](https://nodejs.org/) (Versión recomendada: 18 o superior)
- Un editor de código (recomendamos [VS Code](https://code.visualstudio.com/))

## 🛠️ Pasos para la Instalación

Sigue estos comandos en tu terminal uno por uno:

### 1. Clonar el repositorio
Si aún no tienes el código, clónalo usando Git:
```bash
git clone <URL_DEL_REPOSITORIO>
```
*(Luego entra en la carpeta del proyecto)*:
```bash
cd vite-project
```

### 2. Instalar dependencias
Este comando descargará todas las librerías necesarias para que el proyecto funcione:
```bash
npm install
```

### 3. Ejecutar el proyecto en desarrollo
Una vez instaladas las dependencias, levanta el servidor local:
```bash
npm run dev
```

Cuando veas un mensaje como `Local: http://localhost:5173/`, abre ese enlace en tu navegador.

---

## 📖 Comandos Disponibles

| Comando | Descripción |
| :--- | :--- |
| `npm run dev` | Inicia el servidor de desarrollo con recarga en caliente. |
| `npm run build` | Compila el proyecto para producción (genera la carpeta `dist`). |
| `npm run preview` | Previsualiza la versión de producción localmente. |

## 🛠️ Tecnologías Usadas
- [Vue 3](https://vuejs.org/) (Composition API + `<script setup>`)
- [Vite](https://vitejs.dev/)
- [TypeScript](https://www.typescriptlang.org/)
- [Tailwind CSS](https://tailwindcss.com/)

---

¡Y listo! Ya puedes empezar a trabajar. Si tienes algún problema, no dudes en preguntar. 🚀