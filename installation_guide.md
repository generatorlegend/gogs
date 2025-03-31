# Gogs Installation Guide

This guide provides comprehensive instructions for installing Gogs on different platforms. We'll cover binary installation, Docker deployment, and package manager installation methods. We'll also discuss system requirements and post-installation configuration.

## System Requirements

Before installing Gogs, ensure your system meets the following requirements:

- Database: PostgreSQL, MySQL, SQLite3, or MSSQL
- Git (>= 1.7.1)
- A functioning SSH server (for SSH support)
- Hardware:
  - Minimum: Raspberry Pi or $5 Digital Ocean Droplet
  - Recommended: 2 CPU cores and 512MB RAM for teamwork

## Installation Methods

### 1. Binary Installation

Binary installation is the simplest method for most users.

1. Download the latest Gogs binary for your platform from the [official Gogs downloads page](https://gogs.io/docs/installation/install_from_binary.html).
2. Extract the archive to your desired location.
3. Create a custom configuration file:

```bash
cp /path/to/gogs/custom/conf/app.ini.sample /path/to/gogs/custom/conf/app.ini
```

4. Edit the `app.ini` file to configure your Gogs instance.
5. Run Gogs:

```bash
./gogs web
```

### 2. Docker Installation

For users who prefer containerized deployments, Docker is an excellent option.

1. Pull the Gogs Docker image:

```bash
docker pull gogs/gogs
```

2. Create a volume for persistent data:

```bash
docker volume create gogs-data
```

3. Run the Gogs container:

```bash
docker run --name=gogs -p 10022:22 -p 10080:3000 -v gogs-data:/data gogs/gogs
```

This command maps container port 22 to host port 10022 for SSH and container port 3000 to host port 10080 for HTTP.

### 3. Package Manager Installation

Some platforms offer Gogs through their package managers.

#### Arch Linux

```bash
pacman -S gogs
```

#### FreeBSD

```bash
cd /usr/ports/www/gogs
make install clean
```

## Post-Installation Configuration

After installation, you'll need to configure Gogs:

1. Access the Gogs web interface at `http://localhost:3000` (or the appropriate address if you've configured it differently).
2. Follow the installation wizard to set up your database and admin account.
3. Configure additional settings in the `app.ini` file located in your Gogs custom configuration directory.

Key configuration options include:

- `DOMAIN`: Set this to your public-facing domain name
- `ROOT_URL`: The full public URL of your Gogs instance
- `SSH_DOMAIN`: The domain name to be exposed in SSH clone URLs
- `SSH_PORT`: The port number to be exposed in SSH clone URLs

## Updating Gogs

To update Gogs:

1. Stop the Gogs service.
2. Back up your Gogs installation directory and database.
3. Download and replace the Gogs binary with the latest version.
4. Run any necessary database migrations:

```bash
./gogs admin upgrade
```

5. Restart the Gogs service.

## Troubleshooting

If you encounter issues during installation or configuration:

1. Check the Gogs logs, typically located in `log/gogs.log`.
2. Ensure all system requirements are met.
3. Verify that your `app.ini` configuration is correct.
4. Consult the [Gogs Troubleshooting Guide](https://gogs.io/docs/intro/troubleshooting.html) for common issues and solutions.

For further assistance, you can ask questions in the [Gogs Discussions](https://github.com/gogs/gogs/discussions) on GitHub.