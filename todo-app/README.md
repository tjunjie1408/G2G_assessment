# 📝 Vue 3 Todo App

An elegant, responsive, and fully functional Todo application built with **Vue 3** and **Vite**.

## ✨ Features

- **Add Tasks**: Quickly add new tasks to your list.
- **Mark as Completed**: Toggle task completion status with a single click.
- **Delete Tasks**: Remove tasks you no longer need.
- **Local Storage Persistence**: Your tasks are saved in your browser's local storage, so they won't be lost when you refresh the page.
- **Smooth Animations**: Enjoy fluid transitions when adding or deleting tasks.
- **Responsive Design**: Looks great on both desktop and mobile devices.

## 🚀 Tech Stack

- **[Vue 3](https://vuejs.org/)**: Built using the Composition API and `<script setup>`.
- **[Vite](https://vitejs.dev/)**: Next generation frontend tooling for a lightweight and incredibly fast development server.
- **Custom CSS**: Minimalist custom design without any heavy frameworks.

## 📦 Getting Started

### Prerequisites

You'll need [Node.js](https://nodejs.org/) installed on your machine. We recommend using `pnpm` as the package manager since the `pnpm-lock.yaml` file is provided in this project.

### Installation

1. Navigate to the project directory:
   ```bash
   cd todo-app
   ```

2. Install the dependencies:
   ```bash
   pnpm install
   ```

3. Start the development server:
   ```bash
   pnpm dev
   ```

4. Open your browser and visit `http://localhost:5173` (or the URL provided in your terminal).

## 🛠️ Scripts

- `pnpm dev` - Starts the Vite development server.
- `pnpm build` - Builds the app for production.
- `pnpm preview` - Locally previews the production build.

## 📂 Project Structure

- `src/App.vue`: The main application component containing the state, methods, and UI.
- `src/style.css`: All the application styling rules.
- `index.html`: The HTML entry point for Vite.
- `package.json`: Project metadata and dependencies.
