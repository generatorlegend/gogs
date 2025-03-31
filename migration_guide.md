# Repository Migration Guide

This guide provides instructions on how to migrate repositories from other Git hosting services to Gogs. You'll learn how to import repositories, issues, and pull requests.

## Table of Contents

1. [Importing a Repository](#importing-a-repository)
2. [Migrating Issues and Pull Requests](#migrating-issues-and-pull-requests)
3. [Post-Migration Steps](#post-migration-steps)

## Importing a Repository

To import a repository from another Git hosting service:

1. Log in to your Gogs account.
2. Click on the "+" icon in the top right corner and select "New Migration".
3. Fill in the following details:
   - Clone Address: The URL of the repository you want to migrate.
   - Owner: Select the owner (user or organization) for the new repository.
   - Repository Name: Enter a name for the new repository.
   - Description: (Optional) Add a description for the repository.
   - Private: Check this box if you want the repository to be private.
   - Mirror: Check this box if you want to create a mirror of the original repository.
4. Click "Migrate Repository" to start the migration process.

Example API request for repository migration:

```go
remoteAddr, err := f.ParseRemoteAddr(c.User)
if err != nil {
    // Handle error
}

repo, err := database.MigrateRepository(c.User, ctxUser, database.MigrateRepoOptions{
    Name:        f.RepoName,
    Description: f.Description,
    IsPrivate:   f.Private || conf.Repository.ForcePrivate,
    IsMirror:    f.Mirror,
    RemoteAddr:  remoteAddr,
})
if err != nil {
    // Handle error
}
```

## Migrating Issues and Pull Requests

Currently, Gogs does not provide built-in functionality to automatically migrate issues and pull requests. However, you can follow these steps to manually transfer this information:

1. Export issues and pull requests from your current Git hosting service (if possible).
2. Create new issues in your Gogs repository, copying over the content and metadata from the exported data.
3. For pull requests, you may need to create new branches and open new pull requests in Gogs.

## Post-Migration Steps

After migrating your repository, consider the following steps:

1. Update the repository settings:
   - Go to the repository's "Settings" page.
   - Configure the Issue Tracker and Wiki settings as needed.

2. Set up webhooks and integrations:
   - Navigate to "Settings" > "Webhooks" to configure any necessary webhooks.

3. Update external references:
   - Update any external links or references to point to your new Gogs repository.

4. Verify repository contents:
   - Check that all branches, tags, and commits have been successfully migrated.

5. For mirrored repositories, you can manually trigger a sync:

```go
go database.MirrorQueue.Add(repo.ID)
```

By following these steps, you should be able to successfully migrate your repository to Gogs and continue your development workflow seamlessly.