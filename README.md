# Dolibarr ERP & CRM Project

## Setup instructions

### Create Necessary Directories

If the following directories do not exist, create them. **Do not commit these directories to the repository**, as they contain sensitive information:

- `custom`: Contains custom modules for Dolibarr.
- `documents`: Stores files uploaded and generated via the Dolibarr web interface.
- `mariadb`: Holds the databases and tables for the application.
- `old`: Used for old configurations or backups as necessary.
- `adminer`: Contains a default style, which can be modified or replaced.

### Configure Environment Variables

Create a `.env` file based on `.env.example` by copying it and modifying the values as needed:

```bash
# Rename .env.example to .env
mv .env.example .env
```

Edit the [.env](.env) file and adjust the configuration according to your requirements.

Ensure that the `.env` file does not contain quotes around values, as they may cause issues when loading environment variables.

Example of a valid `.env` file:

```bash
DOLI_COMPANY_NAME=My Company
DOLI_URL_ROOT=erp.mydomain.com
DOLI_DOCKER_PORT=80
```

If your company name contains special characters (e.g., `&`, `=`), wrap it in double quotes:

```bash
DOLI_COMPANY_NAME="Company & Co"
```

### Run Dolibarr

#### With Docker Compose

```bash
# Build and start the Docker containers
docker compose up --build -d
```

```bash
# Stop and remove the Docker containers
docker compose down
```

#### With Setup Script

Alternatively, you can use the `setup.sh` script.

This script will create the necessary directories and launch Docker Compose for you.

```bash
# Grant execute permissions to the setup script
chmod +x setup.sh
# Run the setup script
./setup.sh
```

### Optional: Enable Traefik Support

During the setup process, you will be asked if you want to enable Traefik as a reverse proxy.

If enabled:

- A `compose.override.yml` file will be generated.
- Your `DOLI_COMPANY_NAME` will be transformed (spaces and `-` replaced with `_`).
- Labels for Traefik will be added dynamically.

If you choose not to enable Traefik, the standard setup will proceed without additional proxy settings.
If you're using traefik, don't forget to delete the 'ports' section in `compose.yml`
