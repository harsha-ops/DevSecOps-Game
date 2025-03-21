# Work In Progress 


# Migrating a GitHub CI/CD Pipleine into the Jenkins CI/CD Pipeline.

## Overview

This project is focussed on migrating a Github CI/CD pipeline into the Jenkins CI/CD pipeline which deploys a simple Tic-Tac-Toe gaming application.

![Screenshot 2025-03-04 at 7 16 48 PM](https://github.com/user-attachments/assets/7ed79f9c-9144-4870-accd-500085a15592)

![image](https://github.com/user-attachments/assets/5b2813a5-f493-4665-8964-77359b5be93a)

## Features

- 🎮 Fully functional Tic-Tac-Toe game
- 📊 Score tracking for X, O, and draws
- 📜 Game history with timestamps
- 🏆 Highlights winning combinations
- 🔄 Reset game and statistics
- 📱 Responsive design for all devices

## Technologies Used

- **Frontend**: React, TypeScript, Tailwind CSS
- **CI/CD**: GitHub Actions, Jenkins
- **Containerization**: Docker
- **Deployment**: Kubernetes
- **Static Code Analysis**: ESLint
- **Testing**: Vitest
- **Vulnerability Scanning**: Trivy

## Game Logic

The game implements the following rules:

1. X goes first, followed by O
2. The first player to get 3 of their marks in a row (horizontally, vertically, or diagonally) wins
3. If all 9 squares are filled and no player has 3 marks in a row, the game is a draw
4. Winning combinations are highlighted
5. Game statistics are tracked and displayed

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/devsecops-demo.git
   cd devsecops-demo
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn
   ```

3. Start the development server:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

4. Open your browser and navigate to `http://localhost:5173`

## Building for Production

To create a production build:

```bash
npm run build
# or
yarn build
```

The build artifacts will be stored in the `dist/` directory.


## CI/CD Pipeline

### Jenkins Pipeline

The Jenkins Pipeline includes the following stages:

1. **Unit Testing**: Runs the test suite using Vitest.
2. **Static Code Analysis**: Performs linting with ESLint.
3. **Build**: Creates a production build of the application.
4. **Docker Image Creation**: Builds a Docker image using a multi-stage Dockerfile.
5. **Docker Image Scan**: Scans the image for vulnerabilities using Trivy.
6. **Docker Image Push**: Pushes the image to GitHub Container Registry.
7. **Kubernetes Deployment Update**: Updates the Kubernetes deployment file with the new image tag.

## Deployment

### Kubernetes

### Set up Argo CD:
1. Install Argo CD on the Kubernetes cluster.
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```
2. Set up a Git repository for Argo CD to track the changes in the Kubernetes manifests.

