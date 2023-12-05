
# Neoviz Vue Sample Project

This project demonstrates the integration of Neoviz, a powerful knowledge graph visualization tool, with Vue.js. It provides a working example of how to set up and use Neoviz in a Vue.js application, addressing common challenges and offering a reference for successful compilation and execution.

## Features

- **Vue.js Integration**: The project is built using Vue.js, showcasing how to integrate Neoviz within a Vue application.
- **Neoviz Visualization**: Utilizes Neoviz for graph visualization, demonstrating its setup and usage in a Vue context.
- **Element Plus UI**: Incorporates Element Plus, a Vue-based component library, enhancing the UI and UX of the application.

## Project Structure

- `src/App.vue`: The main Vue component that imports and uses the `MainPage.vue` component.
- `src/components/MainPage.vue`: Contains the core functionality of the Neoviz integration, including graph visualization and interaction logic.
- `src/main.js`: The entry point of the Vue application, setting up Vue and Element Plus.
- `vite.config.js`: Configuration file for Vite, the build tool used in the project.
- `package.json`: Lists the project dependencies and scripts for running the application.

## Setup and Usage

1. **Clone the Repository**: First, clone the repository to your local machine.
2. **Install Dependencies**: Run `npm install` to install the required dependencies.
3. **Run the Application**:
   - For development: `npm run dev` starts the application in development mode with hot-reload.
   - For production: `npm run build` compiles and minifies the production application.
4. **View the Application**: Open the application in a web browser to view and interact with the Neoviz graph.

## Dependencies

- **Vue.js**: A progressive framework for building user interfaces.
- **Neoviz.js**: A JavaScript library for Neo4j graph visualization.
- **Element Plus**: A Vue 3-based component library.

## Recommended IDE Setup

- VSCode with Volar (disabling Vetur) and TypeScript Vue Plugin (Volar).

## Customization and Configuration

The project is tested and configured for Vite and Vue. Users can customize the Neoviz configuration and Vue components as per their requirements.
