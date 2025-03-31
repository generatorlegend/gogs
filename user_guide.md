# Gogs User Guide

## Table of Contents

1. [Introduction](#introduction)
2. [Creating an Account](#creating-an-account)
3. [Creating Repositories](#creating-repositories)
4. [Managing Issues](#managing-issues)
5. [Working with Pull Requests](#working-with-pull-requests)
6. [Collaborating with Other Users](#collaborating-with-other-users)

## Introduction

Gogs is a self-hosted Git service that provides an easy-to-use interface for managing your Git repositories. This user guide will walk you through the basic features and functionalities of Gogs.

## Creating an Account

To get started with Gogs, you need to create an account:

1. Navigate to your Gogs instance's homepage.
2. Click on the "Sign Up" button in the top right corner.
3. Fill in the required information:
   - Username
   - Email address
   - Password
4. If enabled, complete the captcha.
5. Click "Create New Account".

Once your account is created, you may need to verify your email address if email confirmation is required by your Gogs instance.

## Creating Repositories

To create a new repository:

1. Log in to your Gogs account.
2. Click the "+" icon in the top right corner and select "New Repository".
3. Fill in the repository details:
   - Owner (your account or an organization you belong to)
   - Repository name
   - Description (optional)
   - Choose between public or private visibility
4. Optionally, you can initialize the repository with:
   - A README file
   - .gitignore file
   - License
5. Click "Create Repository".

After creation, you'll be redirected to your new repository's page, where you can find instructions on how to push your code.

## Managing Issues

Issues help you track tasks, enhancements, and bugs for your projects:

1. Navigate to your repository.
2. Click on the "Issues" tab.
3. To create a new issue, click "New Issue".
4. Provide a title and description for your issue.
5. Assign labels, milestones, and assignees if needed.
6. Click "Create Issue".

To manage existing issues:

- Use filters to sort and search issues.
- Comment on issues to discuss or provide updates.
- Close issues when they're resolved.
- Reopen closed issues if needed.

## Working with Pull Requests

Pull requests allow you to propose changes to a repository:

1. Fork the repository you want to contribute to.
2. Make your changes in your forked repository.
3. Navigate to the original repository.
4. Click "New Pull Request".
5. Select "compare across forks" and choose your fork as the head repository.
6. Review your changes and click "Create Pull Request".
7. Add a title and description for your pull request.
8. Click "Create Pull Request" to submit.

As a repository maintainer, you can:

- Review incoming pull requests.
- Leave comments and request changes.
- Merge or close pull requests.

## Collaborating with Other Users

Gogs provides several ways to collaborate:

1. **Adding Collaborators**:
   - Go to your repository settings.
   - Click on "Collaborators".
   - Enter the username of the person you want to add.
   - Choose their permission level.

2. **Organizations**:
   - Create an organization for team projects.
   - Add members to the organization.
   - Create team repositories within the organization.

3. **Watching Repositories**:
   - Click the "Watch" button on a repository to receive notifications about activities.

4. **Starring Repositories**:
   - Star repositories to show appreciation and keep track of interesting projects.

Remember to check your Gogs instance's specific settings and features, as some options may be customized or disabled by your administrators.