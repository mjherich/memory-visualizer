# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Development Commands

### Development Server
```bash
npm run dev
```
Starts the Vite development server on port 3000. This is the primary command for local development.

### Build
```bash
npm run build
```
Creates production build in the `dist/` directory using Vite bundler.

### Preview Production Build
```bash
npm run preview
```
Serves the production build locally for testing.

### Install Dependencies
```bash
npm install
```
Install all project dependencies. Run this after cloning or when package.json changes.

## Project Architecture

### Tech Stack
- **Frontend Framework**: React 18 with TypeScript
- **Build Tool**: Vite 5 with React plugin
- **Styling**: TailwindCSS for utility-first CSS
- **Visualization**: D3.js v7 for interactive knowledge graph rendering
- **State Management**: React hooks (useState, useReducer) for local state

### Application Structure
- **Single Page Application**: The app renders one main component `KnowledgeGraphVisualization`
- **Data Processing**: Parses memory.json files with entities and relations in JSONL format (each line is a separate JSON object)
- **Interactive Visualization**: Uses D3.js force simulation to create draggable, zoomable knowledge graphs
- **Navigation History**: Implements browser-like back/forward navigation for selected nodes using useReducer

### Key Components

#### App.tsx
Simple root component that renders the main visualization component.

#### KnowledgeGraphVisualization.tsx
The main component (1100+ lines) that handles:
- **File Upload**: Drag & drop or file picker for memory.json files
- **Data Parsing**: Parses JSONL format with entities and relations
- **D3 Integration**: Creates force-directed graph with nodes and links
- **Filtering**: Search functionality and entity/relation type filters
- **Node Navigation**: Click nodes to view details, with history navigation
- **Responsive Layout**: Adapts to container size changes

### Data Model
The application expects Anthropic Memory MCP format:
- **Entities**: Objects with `type: "entity"`, `name`, `entityType`, `observations[]`
- **Relations**: Objects with `type: "relation"`, `from`, `to`, `relationType`
- **File Format**: JSONL (JSON Lines) - each line contains one entity or relation object

### Key Features
- Interactive D3.js force-directed graph visualization
- Real-time search and filtering
- Node selection with detailed information panel
- History-based navigation (back/forward buttons)
- Drag & drop file upload with paste support
- Responsive design with statistics display
- Zoom and pan functionality
- Automatic graph recentering when nodes are selected

### TypeScript Configuration
- Target: ES2020 with modern DOM APIs
- Strict mode disabled for easier D3.js integration
- Bundler module resolution for Vite compatibility
- React JSX transform enabled

### Development Notes
- Uses refs extensively for D3.js DOM manipulation
- Implements custom history reducer for node navigation
- Handles complex D3 + React integration patterns
- Uses useLayoutEffect for proper dimension calculations
- Implements proper cleanup for D3 simulations and event listeners