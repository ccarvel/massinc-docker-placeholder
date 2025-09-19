# MassInc WordPress Development Environment

A minimal Docker Compose setup for WordPress development with MySQL database and WP-CLI tools.

## Services

- **MySQL 8.0.43** - Database server
- **WordPress (latest)** - WordPress application
- **WP-CLI** - WordPress command-line interface

## The command docker-compose == docker compose 

## Quick Start

1. Start the environment:
   ```bash
   docker-compose up -d
   ```

2. Access WordPress at [http://localhost](http://localhost)

3. Use WP-CLI commands:
   ```bash
   docker-compose run --rm wpcli --info
   ```

## Configuration

### Database
- **Host**: db
- **Database**: wordpress
- **User**: wordpress  
- **Password**: wordpress
- **Root Password**: somewordpress

### Ports
- WordPress: `8001` (http://localhost:8001)
- MySQL: `3306` (accessible from host)

## File Structure

- `./wordpress/` - WordPress files (mounted to container)
- `./uploads.ini` - PHP upload configuration

## WP-CLI Usage

**SUGGEST YOU CREATE AN ALIAS IN YOUR ~/.zshrc or ~/.bashrc**   
```alias dwp='docker-compose run --rm wpcli '```
so after docker compose up -d and initial wordpress setup you can easily use: ```dwp``` to act as ```wp```


The WP-CLI container is configured with the `tools` profile and runs on-demand:

```bash
# Get site info
docker-compose run --rm wpcli --info

# Install WordPress core
docker-compose run --rm wpcli core install --url="http://localhost" --title="Site Title" --admin_user="admin" --admin_password="password" --admin_email="admin@example.com"

# List plugins
docker-compose run --rm wpcli plugin list

# Install a plugin
docker-compose run --rm wpcli plugin install contact-form-7 --activate
```

## Commands

```bash
# Start services
docker-compose up -d

# Stop services  
docker-compose down

# View logs
docker-compose logs -f

# Rebuild containers
docker-compose up -d --build
```

## Notes

- WordPress files persist in the `./wordpress/` directory
- Database data persists in the `db_data` Docker volume
- The MySQL container includes a health check for proper startup sequencing
