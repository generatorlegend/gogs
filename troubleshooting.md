# Troubleshooting Guide

This guide provides solutions for common issues you might encounter while using Gogs. If you're experiencing problems, please refer to the relevant section below.

## Authentication Issues

### Unable to Log In

1. Verify that you're using the correct username and password.
2. Check if your account is activated. If you haven't received an activation email, you can request a new one from the login page.
3. If you've forgotten your password, use the "Forgot Password" option on the login page to reset it.

### Two-Factor Authentication (2FA) Problems

If you're having trouble with 2FA:

1. Ensure your device's time is correctly synchronized.
2. If you've lost access to your 2FA device, use a recovery code to log in.
3. If you don't have recovery codes, contact your Gogs administrator for assistance.

## Repository Access Issues

### Cannot Clone Repository

1. Verify that you have the correct permissions for the repository.
2. Check if you're using the correct URL for cloning (HTTPS or SSH).
3. For SSH, ensure your SSH key is added to your Gogs account.

### Push Rejected

If your push is rejected:

1. Pull the latest changes from the remote repository first.
2. Check if you have write permissions for the repository.
3. Verify that your local branch is not behind the remote branch.

## Performance Concerns

### Slow Web Interface

If the Gogs web interface is running slowly:

1. Check your internet connection.
2. Clear your browser cache and cookies.
3. If the problem persists, it might be a server-side issue. Contact your Gogs administrator.

### Slow Git Operations

For slow git operations:

1. Check your internet connection speed.
2. For large repositories, try using shallow clones (`git clone --depth 1`).
3. If the issue persists, it could be related to server resources. Contact your Gogs administrator.

## Configuration Issues

### Email Notifications Not Received

If you're not receiving email notifications:

1. Check your spam folder.
2. Verify that your email address is correctly set in your Gogs profile.
3. Ensure that email services are properly configured in the Gogs `app.ini` file:

```ini
[email]
ENABLED = true
HOST = your-smtp-server:port
FROM = your-email@example.com
USER = your-smtp-username
PASSWD = your-smtp-password
```

### SSH Key Problems

If you're having issues with SSH keys:

1. Ensure your SSH key is correctly added to your Gogs account.
2. Check if your SSH key is valid and has the correct permissions:

```bash
chmod 600 ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa
```

3. Test your SSH connection:

```bash
ssh -T git@your-gogs-instance.com
```

## Server-Side Issues

If you're a Gogs administrator and encountering server-side problems:

### Database Connection Errors

1. Check if the database server is running.
2. Verify the database connection settings in `app.ini`:

```ini
[database]
TYPE = mysql
HOST = 127.0.0.1:3306
NAME = gogs
USER = gogs
PASSWD = your-password
```

### Git Errors

If you're seeing Git-related errors in the logs:

1. Ensure Git is properly installed on the server.
2. Check Git-related settings in `app.ini`:

```ini
[git]
; Disables highlight of added and removed changes
DISABLE_DIFF_HIGHLIGHT = false
; Max number of files shown in diff view
MAX_GIT_DIFF_FILES = 100
; Max number of lines allowed of a single file in diff view
MAX_GIT_DIFF_LINES = 1000
```

### Logging

If you need to troubleshoot further, check the Gogs log files. The location and level of logging can be configured in `app.ini`:

```ini
[log]
ROOT_PATH = /path/to/logs
MODE = file
LEVEL = Info
```

## Still Need Help?

If you're still experiencing issues after trying these troubleshooting steps, consider:

1. Checking the [Gogs issue tracker](https://github.com/gogs/gogs/issues) for similar problems and solutions.
2. Asking for help in the [Gogs community forums](https://discuss.gogs.io/).
3. If you believe you've found a bug, report it on the [Gogs GitHub repository](https://github.com/gogs/gogs/issues/new).

Remember to provide as much detail as possible when seeking help, including your Gogs version, operating system, and any relevant log entries or error messages.