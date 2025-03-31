# API Reference

This page provides a comprehensive reference of all public API endpoints in Gogs. It includes information on authentication, request/response formats, and example usage for each endpoint.

## Table of Contents

1. [Authentication](#authentication)
2. [Users](#users)
3. [Repositories](#repositories)
4. [Organizations](#organizations)
5. [Issues](#issues)
6. [Miscellaneous](#miscellaneous)

## Authentication

Gogs API supports two types of authentication:

1. Access Token
2. Basic Authentication

Most endpoints require authentication using one of these methods.

### Access Token

To use an access token, include it in the `Authorization` header:

```
Authorization: token YOUR_ACCESS_TOKEN
```

### Basic Authentication

For Basic Authentication, include your username and password in the `Authorization` header:

```
Authorization: Basic BASE64_ENCODED_USERNAME_PASSWORD
```

## Users

### Search Users

```
GET /api/v1/users/search
```

Search for users by username.

#### Parameters

| Name     | Type   | Description           |
|----------|--------|-----------------------|
| q        | string | Search keyword        |
| limit    | int    | Maximum number of users to return (default: 10) |

#### Example

```bash
curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
     https://try.gogs.io/api/v1/users/search?q=john&limit=5
```

### Get User Information

```
GET /api/v1/users/:username
```

Get information about a user.

#### Example

```bash
curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
     https://try.gogs.io/api/v1/users/johndoe
```

## Repositories

### List User Repositories

```
GET /api/v1/users/:username/repos
```

List repositories owned by a user.

#### Example

```bash
curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
     https://try.gogs.io/api/v1/users/johndoe/repos
```

### Create Repository

```
POST /api/v1/user/repos
```

Create a new repository for the authenticated user.

#### Parameters

| Name        | Type    | Description                                |
|-------------|---------|--------------------------------------------|
| name        | string  | The name of the repository                 |
| description | string  | A short description of the repository      |
| private     | boolean | Whether the repository is private or public |

#### Example

```bash
curl -X POST -H "Authorization: token YOUR_ACCESS_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"name": "new-repo", "description": "My new repository", "private": false}' \
     https://try.gogs.io/api/v1/user/repos
```

## Organizations

### List User Organizations

```
GET /api/v1/users/:username/orgs
```

List organizations that a user belongs to.

#### Example

```bash
curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
     https://try.gogs.io/api/v1/users/johndoe/orgs
```

### Create Organization

```
POST /api/v1/user/orgs
```

Create a new organization for the authenticated user.

#### Parameters

| Name        | Type   | Description                           |
|-------------|--------|---------------------------------------|
| username    | string | The username of the new organization  |
| full_name   | string | The full name of the organization     |
| description | string | A description of the organization     |

#### Example

```bash
curl -X POST -H "Authorization: token YOUR_ACCESS_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"username": "new-org", "full_name": "New Organization", "description": "A new organization"}' \
     https://try.gogs.io/api/v1/user/orgs
```

## Issues

### List Repository Issues

```
GET /api/v1/repos/:username/:reponame/issues
```

List issues for a repository.

#### Parameters

| Name   | Type   | Description                                  |
|--------|--------|----------------------------------------------|
| state  | string | State of issues to return. Can be open, closed or all. Default: open |
| labels | string | Comma-separated list of label names to filter by |
| sort   | string | What to sort results by. Can be created, updated, comments. Default: created |
| since  | string | Only show notifications updated after the given time. This is a timestamp in ISO 8601 format: YYYY-MM-DDTHH:MM:SSZ |

#### Example

```bash
curl -H "Authorization: token YOUR_ACCESS_TOKEN" \
     https://try.gogs.io/api/v1/repos/gogs/gogs/issues?state=open&labels=bug
```

### Create Issue

```
POST /api/v1/repos/:username/:reponame/issues
```

Create a new issue in a repository.

#### Parameters

| Name    | Type   | Description              |
|---------|--------|--------------------------|
| title   | string | The title of the issue   |
| body    | string | The body of the issue    |
| assignee| string | Login for the user that this issue should be assigned to |
| milestone| int   | The number of the milestone to associate this issue with |
| labels  | array  | Labels to associate with this issue |

#### Example

```bash
curl -X POST -H "Authorization: token YOUR_ACCESS_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"title": "New bug", "body": "Please fix this bug", "assignee": "johndoe", "labels": ["bug", "important"]}' \
     https://try.gogs.io/api/v1/repos/gogs/gogs/issues
```

## Miscellaneous

### Render Markdown

```
POST /api/v1/markdown
```

Render a Markdown document.

#### Parameters

| Name    | Type   | Description              |
|---------|--------|--------------------------|
| text    | string | The Markdown text to render |
| mode    | string | The rendering mode. Can be 'markdown' or 'gfm' |
| context | string | The repository context, only taken into account for 'gfm' mode |

#### Example

```bash
curl -X POST -H "Authorization: token YOUR_ACCESS_TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"text": "# Hello\n\nThis is a test.", "mode": "markdown"}' \
     https://try.gogs.io/api/v1/markdown
```

This API reference provides an overview of the main endpoints available in the Gogs API. For more detailed information about specific endpoints, request/response formats, and additional parameters, please refer to the source code or contact the Gogs development team.