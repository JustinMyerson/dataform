---
title: Git access tokens
subtitle: Learn how to use Git access tokens for connecting to git providers.
priority: 1
---

Git access tokens are important for Dataform projects linked to remote git providers, such as GitHub. They provide authentication for accessing and controlling the git project.

<div className="bp3-callout bp3-icon-info-sign bp3-intent-warning" markdown="1">
  Dataform's IP addresses may need be allowlisted in order to access your GitHub / GitLab repository cluster. Dataform's IP addresses are <code>35.233.106.210</code> and <code>104.196.10.242</code>.
</div>

## User authentication

User access tokens are used to authenticate git access of Dataform projects during project manipulation.

Without a valid access token, users will be unable to do things such as create branches.

They must be configured to have both **read and write access** to your remote repository.

They can be added or removed on the **user settings page**.

## Scheduler authentication

Scheduler access tokens are used to authenticate git access of Dataform projects when running automated schedules.

Without a valid access token, the scheduler will not be able to read the contents of the project and perform the run.

They must have **read** access to your remote repository.

<div className="bp3-callout bp3-icon-info-sign bp3-intent-warning" markdown="1">
  GitHub doesn't support read-only access to the repo. You should use the <code>repo</code> <a target="_blank" rel="noopener" href="https://developer.github.com/apps/building-oauth-apps/understanding-scopes-for-oauth-apps">scope</a>
</div>

They can be updated on the **project settings page**, within the app.

For projects with only a few collaborators (e.g. 3), it's ok to use a user's personal access token to authenticate the scheduler, but for larger teams a **machine user** is recommended. If you have a DevOps team, ask them about whether a machine user already exists.

### Machine user

Machine users are generally regular user accounts, but used purely to run automated (or triggered) tasks.

If a user's personal access token is used and they leave the organization or their permission is revoked, then the scheduler will fail.

Because of this, **we recommend to have a global machine user on organization level, to make sure there is no disruption during scheduling**.

Check [this](https://developer.github.com/v3/guides/managing-deploy-keys/#machine-users) for further info on creating machine users.

Before creating a machine user on GitHub, please read their [TOCs](https://help.github.com/en/github/site-policy/github-terms-of-service#3-account-requirements).

## Creating git access tokens

How to create a git access token differs between remote git providers.

### GitHub

[Creating a **GitHub** personal access token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#creating-a-token).

Permissions required:
 - repo

### GitLab

[Creating a **GitLab** personal access token](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#creating-a-personal-access-token). The access token name must be `dataform`. You must have `maintainer` permissions on the repo.

Permissions required:
 - api
 - read_repository
 - write_repository

### Azure Repo

[Creating a **Azure DevOps** personal access token](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=preview-page#create-a-pat ).

Permissions required:
 - code:full

