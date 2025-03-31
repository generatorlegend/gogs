# Authentication Methods in Gogs

Gogs supports multiple authentication methods to provide flexibility and security for users. This document explains the different authentication methods available and provides setup instructions for each.

## Local Authentication

Local authentication is the default method used by Gogs. It stores user credentials in the Gogs database.

### Setup

1. Local authentication is enabled by default.
2. To customize settings, edit the `[auth]` section in `conf/app.ini`:

```ini
[auth]
REQUIRE_EMAIL_CONFIRMATION = false
DISABLE_REGISTRATION = false
ENABLE_REGISTRATION_CAPTCHA = true
```

- `REQUIRE_EMAIL_CONFIRMATION`: Set to `true` to require email confirmation for new registrations.
- `DISABLE_REGISTRATION`: Set to `true` to disable self-registration.
- `ENABLE_REGISTRATION_CAPTCHA`: Set to `true` to enable CAPTCHA for registration.

## LDAP Authentication

LDAP (Lightweight Directory Access Protocol) authentication allows Gogs to authenticate users against an LDAP server.

### Setup

1. Enable LDAP authentication by adding an LDAP source in the admin panel.
2. Configure LDAP settings in `conf/app.ini`:

```ini
[auth.ldap]
ENABLED = true
HOST = ldap.example.com
PORT = 389
USE_SSL = false
BIND_DN = cn=admin,dc=example,dc=com
BIND_PASSWORD = admin_password
USER_BASE = ou=Users,dc=example,dc=com
USER_FILTER = (&(objectClass=posixAccount)(uid=%s))
```

Adjust the settings according to your LDAP server configuration.

## OAuth Authentication

Gogs supports OAuth 2.0 authentication with various providers such as GitHub, GitLab, and Google.

### Setup

1. Register your Gogs instance as an OAuth application with the desired provider.
2. Configure OAuth settings in `conf/app.ini`:

```ini
[oauth2]
ENABLED = true

[oauth2.github]
ENABLED = true
CLIENT_ID = your_client_id
CLIENT_SECRET = your_client_secret
SCOPES = user:email
```

Replace `your_client_id` and `your_client_secret` with the credentials obtained from the OAuth provider.

3. Repeat the configuration for other OAuth providers as needed.

## Two-Factor Authentication (2FA)

Gogs supports two-factor authentication for added security.

### Setup

1. Enable 2FA in `conf/app.ini`:

```ini
[security]
ENABLE_TWO_FACTOR_AUTH = true
```

2. Users can enable 2FA in their account settings.

## Reverse Proxy Authentication

Gogs can be configured to use reverse proxy authentication, allowing authentication to be handled by an external service.

### Setup

1. Configure reverse proxy authentication in `conf/app.ini`:

```ini
[auth]
ENABLE_REVERSE_PROXY_AUTHENTICATION = true
ENABLE_REVERSE_PROXY_AUTO_REGISTRATION = true
REVERSE_PROXY_AUTHENTICATION_HEADER = X-WEBAUTH-USER
```

2. Ensure your reverse proxy is properly configured to set the authentication header.

## Conclusion

Gogs provides various authentication methods to suit different deployment scenarios and security requirements. Choose the method that best fits your needs and configure it accordingly.

For more detailed information on each authentication method, refer to the Gogs documentation or consult the source code in the `internal/auth` package.