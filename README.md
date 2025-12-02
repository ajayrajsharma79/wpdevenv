# WordPress Development Environment

This project provides a complete local development environment for WordPress using Docker. It includes custom-built containers for MariaDB, WordPress, and phpMyAdmin, all based on `debian:trixie-slim`.

## Features

- **Custom Docker Images**: Lightweight images based on Debian Trixie Slim.
- **Persistent Storage**: 
  - WordPress files are mounted locally in `wordpress_data/` for easy theme/plugin development.
  - Database files are persisted in `mariadb_data/`.
- **Environment Configuration**: All sensitive configuration is managed via `.env` file.
- **Tools**: Includes phpMyAdmin for database management.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1.  **Clone the repository** (if applicable).

2.  **Configure Environment Variables**:
    Copy the example environment file to create your local configuration:
    ```bash
    cp .env.example .env
    ```
    You can edit `.env` to change database credentials or other settings if needed.

3.  **Build and Start Containers**:
    Run the following command to build the images and start the services:
    ```bash
    docker-compose up -d --build
    ```

4.  **Access the Services**:
    - **WordPress**: [http://localhost:8080](http://localhost:8080)
    - **phpMyAdmin**: [http://localhost:8081](http://localhost:8081)
    - **MariaDB**: Port `3306`

## Directory Structure

- `mariadb/`: Dockerfile and entrypoint for the MariaDB service.
- `wordpress/`: Dockerfile and entrypoint for the WordPress service.
- `phpmyadmin/`: Dockerfile and entrypoint for the phpMyAdmin service.
- `mariadb_data/`: Local directory where database files are stored (ignored by git).
- `wordpress_data/`: Local directory where WordPress files are stored (ignored by git).
- `docker-compose.yml`: Defines the services and their relationships.

## Development

- **WordPress Files**: The `wordpress_data` directory is mapped to `/var/www/html` in the container. Any changes you make to files in this directory (e.g., creating a new theme or plugin) will be immediately reflected in the running WordPress instance.
- **Database**: The `mariadb_data` directory persists your database changes across container restarts and rebuilds.

## Stopping the Environment

To stop the containers:
```bash
docker-compose down
```

To stop the containers and remove volumes (WARNING: this will delete your database and wordpress files if you haven't backed them up, although the bind mounts usually persist on the host):
```bash
docker-compose down -v
```

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

