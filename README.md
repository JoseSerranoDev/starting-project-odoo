# Odoo Project

This is an Odoo project setup using Docker and Docker Compose. Follow the steps below to get it running on your local machine.

---

## Installation

### Prerequisites
Before starting, make sure you have installed the following:

- Docker >= 24.x
- Docker Compose >= 2.x
- Git

---

### 1. Clone the repository
Clone the project from GitHub and enter the project folder:

```bash
git clone https://github.com/yourusername/yourrepository.git
cd yourrepository
```

### 2. Configure environment variables

This project uses a .env file for configuration.
A sample file is provided as .env.sample. You need to create a .env file in the project root based on it:

```bash
cp .env.sample .env
```
Then, edit .env to customize your database credentials, ports, or other settings if necessary.

### 3. Build and start the Docker containers:

Run the following command to build and start Odoo and PostgreSQL containers:

```bash
docker-compose up --build
```

Add the `-d` flag to run the containers in detached mode:

```bash
docker-compose up -d --build
```

### 4. Access the Odoo instance:

Open your web browser and navigate to http://localhost:8070.

### 5. Log in to Odoo:

You can use the default credentials to log in:

    - User: admin
    - Password: admin

---

# Useful commands

## Start containers in detached mode

docker compose up -d

## Stop and remove containers

docker compose down

## Update a specific Odoo module

docker exec -it odoo-app sh -c "odoo -d {db_name} --db_host=db --db_user={db_user} --db_password={db_password} --addons-path=/mnt/extra-addons -u {module_name} --stop-after-init"

docker exec -it odoo-app sh -c "odoo -d odoo_db --db_host=db --db_user=odoo_user --db_password=changeme --addons-path=/mnt/extra-addons -u estate --stop-after-init"

## Access PostgreSQL shell

docker exec -it {container_name} psql -U {user} -d {database}

docker exec -it odoo-db psql -U odoo_user -d odoo_db
