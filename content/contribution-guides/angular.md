---
title: Angular projects
navigation.icon: vscode-icons:file-type-angular
---

# Angular projects

We are really excited that you are interested in contributing. This is a general contribution guide for ArmoniK's projects written with the Angular Framework.
Before submitting your contribution, please make sure to take a moment and read through the following guide:

## 🧑‍💻 Repository Setup

We use [pnpm](https://pnpm.io) for every project. We highly recommand you install [ni](https://github.com/antfu/ni) so you don't worry about the package manager when switching across different projects.

We will use ni's commands in the following code snippets. If you are not using it, you can do the conversion yourself: `ni = pnpm install`, `nr = pnpm run`.

To set the repository up:

| Step                                           | Command              |
|------------------------------------------------|----------------------|
| 1. Install Node.js, using the latest LTS       | -                    |
| 2. Enable Corepack                             | `corepack enable`    |
| 3. Install @antfu/ni                           | `npm i -g @antfu/ni` |
| 4. Install dependencies under the project root | `ni`                 |

## 🗃️ Repository Structure

We use vanilla Angular CLI to generate projects (applications or libraries).

```bash
ng new <project-name> --standalone
```

We do not use Nx for our new projects because of the complexity it adds to the project.

We try to stay as close as possible to the [Angular Style Guide](https://angular.io/guide/styleguide). We use [ESLint](https://eslint.org/) to enforce the style guide.

We use [standalone components](https://angular.io/guide/standalone-components) for every component we create. We use [inline-template](https://angular.io/guide/standalone-components#inline-template) and [inline-style](https://angular.io/guide/standalone-components#inline-style) for every component we create.

For the UI, we use [Angular Material](https://material.angular.io/). We use [Angular CDK](https://material.angular.io/cdk/categories) for the components that are not available in Angular Material.

Finally, we try to stay as close as possible up-to-date with the latest Angular and Angular Material version.

::alert{type="info"}
Staying up to date is important for security reasons and possible due to the use of Angular packages for the UI (which are updated within Angular update).
::

## 💡 Commands

We follow the [Angular CLI](https://angular.io/cli) commands.

## 📚 Documentation

Please refer to [the contribution guide about documentation](./documentation.md).

## 🙌 Sending Pull Request

Please refer to related release processes:

- [Discuss First](../working-processes/discuss-first.md)
- [Submission Guidelines](../working-processes/submission-guidelines.md)

## 👩‍🔧 Maintenance

This section is for maintainers with write access, or if you want to maintain your own forks.

### Update Dependencies

Keeping dependencies up-to-date is one of the important aspects to keep projects alive and getting latest bug fixes on time. We recommend to update dependencies in weekly or bi-weekly intervals.

We use [taze](https://github.com/antfu/taze) to update the dependencies manually most of the time. To automatically update dependencies, we use [Renovate](https://renovatebot.com/).

With `taze`, you can run `taze major -Ir` to check and select the versions to update interactive. `-I` stands for `--interactive`, `-r` stands for `--recursive` for monorepo.

You can use `taze` with [npx](https://docs.npmjs.com/cli/v9/commands/npx): `npx taze@latest`

After bumpping, we remove lock file, we install them, runing build and test to verify nothing breaks before creating a Pull Request.

### Releasing

Please refer to [release processes](../working-processes/release-processes.md) in our working processes.

> This guide is heavily inpired by the contribute from [@antfu](https://github.com/antfu/).
