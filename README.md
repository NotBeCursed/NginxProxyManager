# Nginx Proxy Manager Docker Stack

**Nginx Proxy Manager** (NPM) is an easy-to-use solution for managing Nginx proxy servers. It allows you to manage HTTP, HTTPS, and WebSocket proxies via a web interface. This Docker stack configures Nginx Proxy Manager to handle and automate the setup of your Nginx server.

## Prerequisites

- **Docker** and **Docker Compose** installed on your system.
- A **domain name** configured (optional, but recommended if you plan to use SSL).
- A **MariaDB database** to store Nginx Proxy Manager data.

## Stack Overview

- **Nginx Proxy Manager (NPM)**: Provides a web interface to manage Nginx reverse proxies.
- **MariaDB**: The database used by NPM to store configuration data.

## Installation 
Clone this repository to your local machine:

```bash
    git clone https://github.com/NotBeCursed/NginxProxyManager.git
    cd NginxProxyManager
```

## Configuration

### 1. Create a `.env` file

For secure and flexible configuration, we use a `.env` file to manage environment variables. Here's an example of what it should contain:

```ini
# MySQL Database Configuration
DB_MYSQL_HOST=db
DB_MYSQL_PORT=3306
DB_MYSQL_USER=your_mysql_user
DB_MYSQL_PASSWORD=your_mysql_password
DB_MYSQL_NAME=nginx_proxy_manager_db

# MariaDB Configuration
MYSQL_ROOT_PASSWORD=root_password
MYSQL_DATABASE=nginx_proxy_manager
MYSQL_USER=your_mysql_user
MYSQL_PASSWORD=your_mysql_password
```
Make sure to replace these values with your own configuration.

### 2. Start the Stack

After configuring your `.env` file and `docker-compose.yml`, you can start the stack with the following command:

```bash
docker-compose up -d
```

This will:

- Start **Nginx Proxy Manager** on ports `80`, `443`, and `81`.
- Start **MariaDB** to store NPM's data.

### 3. Access the Admin Interface

Once the containers are up and running, you can access the Nginx Proxy Manager web interface by visiting:

```
http://localhost:81
```

The default login credentials are:

- **Username**: `admin@example.com`
- **Password**: `changeme`

It is highly recommended to change these credentials immediately after the first login.

### 4. Configuring SSL (Optional)

Nginx Proxy Manager supports easy SSL configuration with Let's Encrypt. To enable SSL for a site:

1. Create a **Proxy Host** in the NPM web interface.
2. In the SSL options, check **Request a new SSL certificate**.
3. NPM will automatically generate an SSL certificate for your domain.

### 5. Adding a Proxy Host

Once logged into the NPM web interface:

1. Go to **Proxy Hosts**.
2. Click **Add Proxy Host**.
3. Fill in the required details:
   - **Domain Names**: The domain name of your site (e.g., `yourdomain.com`).
   - **Forward Hostname / IP**: The address of the backend service or server (e.g., `192.168.1.100`).
   - **Forward Port**: The port on which the backend service is running (e.g., `8080`).
   - Enable SSL if required.
4. Click **Save**.

### 6. Manually Adding SSL Certificates (Optional)

If you prefer to add SSL certificates manually, place them in the `/etc/letsencrypt` directory of the **nginx_app** container. You can then configure the virtual hosts to use these certificates.

## Troubleshooting

- **Ports already in use**: If you encounter an error stating that ports `80`, `443`, or `81` are already in use, make sure no other web services are running on those ports.
  
- **Database not starting**: If the database container fails to start, check the logs with `docker-compose logs db` for any configuration errors.

- **Nginx Proxy Manager not working**: Check the logs for the application with `docker-compose logs app` to identify any issues with the database connection or application startup.

## License
This project is licensed under the MIT License - see the LICENSE file for details.
- **Nginx Proxy Manager** is open-source and licensed under the **MIT License**.
- **MariaDB** is licensed under the **GPLv2**.

For more information, refer to the respective documentation:

- [Nginx Proxy Manager Documentation](https://nginxproxymanager.com/)
- [MariaDB Documentation](https://mariadb.org/documentation/)

