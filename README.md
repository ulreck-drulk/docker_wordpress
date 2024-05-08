# Docker Compose WordPress Setup

This Docker Compose configuration sets up a WordPress instance with MySQL using Docker Compose. It includes two services, `wordpress` and `mysql`, and configures them to communicate over a custom network named `rogernet`.

## Prerequisites

Before running this setup, make sure you have Docker and Docker Compose installed on your machine.

## Usage

1. Clone this repository to your local machine or create a directory and create a `docker-compose.yaml` file with the provided content.

2. Navigate to the directory containing the `docker-compose.yaml` file.

3. Run the following command to start the WordPress and MySQL containers:

   ```bash

   docker compose up -d

This command will create and start the containers defined in the docker-compose.yaml file. The -d flag runs the containers in detached mode, meaning they will run in the background.

1. Access your WordPress site in a web browser by visiting http://localhost:8089. F
2. Follow the WordPress setup instructions to complete the installation.
3. Once you're done, you can stop and remove the containers by running:

    ```bash

    docker-compose down

This command will stop and remove the containers but retain the data volumes, so your WordPress site's data will persist.

Configuration Details

    WordPress Service (wordpress):
        Container Name: frontend
        Image: wordpress
        Ports: Exposes port 8089 on the host, mapping it to port 80 in the container.
        Environment Variables:
            WORDPRESS_DB_HOST: Specifies the hostname of the MySQL database container (backend).
            WORDPRESS_DB_USER: Specifies the MySQL database user (root).
            WORDPRESS_DB_PASSWORD: Specifies the MySQL database password (password).
            WORDPRESS_DB_NAME: Specifies the name of the WordPress database (wordpress).
        Depends On: Ensures that the wordpress service starts after the mysql service.

    MySQL Service (mysql):
        Container Name: backend
        Image: mysql
        Environment Variables:
            MYSQL_ROOT_PASSWORD: Specifies the root password for the MySQL server (password).
            MYSQL_DATABASE: Specifies the name of the WordPress database (wordpress).
            MYSQL_PASSWORD: Specifies the password for the MySQL user (wordpress).
        Volumes: Mounts the ./mysql directory on the host to /var/lib/mysql in the container, allowing data persistence.
        Restart Policy: always ensures that the container restarts automatically if it stops.

Network Configuration

    Custom Network (rogernet):
        IP Address Management (IPAM):
            Driver: Default
            Configuration: Defines a subnet (192.168.12.0/24) for the custom network.

Disclaimer

This setup is intended for local development and testing purposes only. It's important to use secure configurations and best practices when deploying applications in production environments.
