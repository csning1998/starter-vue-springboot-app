# Project with Dev Stack of Vue + Vite + TypeScript + Spring Boot + IBM DB2

---

## Overview

This project is a modern web application stack leveraging the following technologies:

- **Frontend**: Vue.js (using Vite as the build tool) with TypeScript.
- **Backend**: Spring Boot framework.
- **Database**: IBM DB2, configured and managed via Docker.

The project is containerized with Docker Compose to streamline setup and deployment, supporting both development and production environments.

---

## Setup and Usage

### 1. Clone the Repository

```bash
git clone https://github.com/csning1998/internship-vue-springboot-api-app.git
cd Internship
```

### 2. Configure Environment Variables

The project requires environment variables for different configurations. Follow these steps:

1. Create a `.env` file in the root directory using the provided `.env-sample` file:

    ```bash
    cp .env-sample .env
    ```

2. Edit the `.env` file to match your setup. For environment-specific configurations, use `.env.dev` and `.env.prod` as needed.

### 3. Build and Start the Project with Docker

#### **Development Environment**

For development, use the `.env.dev` file:

```bash
docker compose --env-file .env.dev up --build
```

This command will:

- Build the Docker images for the backend and frontend.
- Initialize the IBM DB2 database and apply configurations.
- Start the required services: **frontend**, **backend**, and **database**.

Subsequent starts without rebuilding:

```bash
docker compose --env-file .env.dev up
```

#### **Production Environment**

For production, use the `.env.prod` file:

```bash
docker compose --env-file .env.prod up --build
```

Subsequent starts without rebuilding:

```bash
docker compose --env-file .env.prod up
```

### 4. Access the Application

- **Frontend**: [http://localhost:8080](http://localhost:8080)
- **Backend API**: [http://localhost:8443](http://localhost:8443)

### 5. Testing and Validation

- The backend service includes a health check endpoint to ensure connectivity with the database.
- Frontend functionality can be tested by accessing the UI and validating dynamic interactions.

### 6. Logs and Debugging

- View container logs using:
  ```bash
  docker compose logs -f <service-name>
  ```

  Replace `<service-name>` with `frontend`, `backend`, or `db2instance` as needed.

- If any service fails to start, check the logs for errors and verify the `.env` configuration.

---

## Advanced Topics

### Customizing the Environment

For advanced users, you can define multiple `.env` files for different environments (e.g., `.env.dev`, `.env.prod`). Use the appropriate file by setting the `--env-file` flag:

```bash
docker compose --env-file .env.prod up
```

### Database Management

To connect to the IBM DB2 database manually for queries or management:

1. Enter the DB2 container:
    ```bash
    docker exec -it <db2-container-name> bash
    ```

2. Connect to the database:
    ```bash
    db2 connect to TESTDB user <username> using <password>
    ```

### Rebuilding the Database

If database initialization fails or a clean reset is required, remove the database volume:

```bash
docker compose down -v
```

This will delete all database data. Re-run the appropriate `docker compose up --build` command to reinitialize.

---

## Troubleshooting

### Common Issues

- **Frontend not accessible at `localhost:8080`**: Ensure the `frontend` service is running and no other application is occupying port 8080.
- **Backend API issues**: Verify that the `backend` service can connect to the database by checking logs for connection errors.
- **Database setup issues**: Confirm that the `db2instance` container has initialized correctly and the database is active.

### Useful Commands

- Stop all services:
  ```bash
  docker compose down
  ```

- Remove all containers and volumes:
  ```bash
  docker compose down -v
  ```

- Rebuild a specific service:
  ```bash
  docker compose up --build <service-name>
  ```

---

## Contributing

Contributions to the project are welcome! To get started:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request with a clear description of your changes.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.