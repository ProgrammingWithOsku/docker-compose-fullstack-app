
# Vidly Full-Stack Application with Docker Compose

This project is a demo of a full-stack application using React for the frontend, Node.js for the backend, and MongoDB as the database. The entire application is containerized using Docker and managed with Docker Compose.

## Project Structure

- **frontend/**: Contains the React code for the frontend.
- **backend/**: Contains the Node.js/Express code for the backend.
- **docker-compose.yml**: Docker Compose configuration to orchestrate frontend, backend, and MongoDB containers.
- **MongoDB**: Used as the database for storing application data.

## Prerequisites

Ensure you have the following installed on your machine:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Node.js](https://nodejs.org/en/) (for installing dependencies locally)

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/vidly-fullstack-docker.git
cd vidly-fullstack-docker
```

### 2. Install Dependencies Locally

To ensure that changes are properly reflected during development, you need to install the project dependencies on your local machine. This step is important because Docker mounts your local project directory into the container, and if `node_modules` isn't present locally, you may encounter issues.

- Navigate to the `frontend` directory and run:

  ```bash
  cd frontend
  npm install
  ```

- Navigate to the `backend` directory and run:

  ```bash
  cd ../backend
  npm install
  ```

**Reminder:** This step is necessary to prevent issues with reflecting code changes in your Docker container. If you skip this step, you might encounter errors due to missing local dependencies.

### 3. Build and Run the Application

To build and run the application, navigate to the root directory (where the `docker-compose.yml` file is located) and run the following command:

```bash
docker-compose up --build
```

This command will:

- Build the frontend (React) Docker image.
- Build the backend (Node.js) Docker image.
- Start a MongoDB container for the database.
- Mount your local code to the containers so that changes are reflected automatically (hot-reload).

### 4. Access the Application

Once the containers are up and running:

- **Frontend**: Open your browser and go to `http://localhost:4000`. This is where the React frontend is served.
- **Backend**: The backend is running on `http://localhost:3001`. However, you will mostly interact with it via the frontend or APIs.
- **MongoDB**: The MongoDB instance is available internally to the backend service at `mongodb://db/vidly`.

### 5. Stopping the Application

To stop the application and remove the containers, run:

```bash
docker-compose down
```

This will stop and remove all containers, networks, and volumes created by Docker Compose.

## Project Overview

### Frontend

- The frontend is built with React using `create-react-app`.
- It serves as the user interface for the application, allowing users to interact with the data stored in MongoDB via the backend.

### Backend

- The backend is built with Node.js and Express.
- It provides a RESTful API for the frontend to interact with the MongoDB database.
- It connects to MongoDB using the connection string defined in the `docker-compose.yml` file (`DB_URL`).

### MongoDB

- MongoDB is used as the primary database.
- The data is persisted using a Docker volume, so the data remains even if the MongoDB container is stopped or removed.

## Development Mode

During development, the code is mounted as volumes inside the containers. This allows you to make changes to the code on your local machine, and the changes will be reflected automatically inside the containers without needing to rebuild them.

For React, file changes are detected using polling (`CHOKIDAR_USEPOLLING=true`), which ensures that hot-reloading works properly in Docker.

### Environment Variables

The following environment variables are set for the frontend and backend services:

- **CHOKIDAR_USEPOLLING=true**: Ensures reliable file watching inside Docker for React.
- **CI=true**: Disables interactive prompts and browser auto-opening in React when running inside Docker.

## Troubleshooting

- **Frontend Not Refreshing Automatically**: Ensure that `CHOKIDAR_USEPOLLING=true` is set in the `docker-compose.yml` file to enable file polling for React in Docker.
- **Port Conflicts**: Ensure that no other services are running on ports `3000` (for frontend) and `3001` (for backend). You can modify the port mappings in the `docker-compose.yml` file if needed.
- **Database Connection Issues**: Check that the `DB_URL` environment variable is set correctly and that the `db` service is running properly.
- **Missing Local Dependencies**: Make sure to run `npm install` in both the `frontend` and `backend` directories on your local machine to avoid issues with reflecting changes in Docker.

