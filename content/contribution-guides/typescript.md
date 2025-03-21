---
title: TypeScript projects
navigation.icon: vscode-icons:file-type-typescript-official
---

# TypeScript projects

We are really excited that you are interested in contributing. This is a general contribution guide for ArmoniK's projects written in TypeScript. Before submitting your contribution, please make sure to take a moment and read through the following guide:

## 🧑‍💻 Repository Setup

We use [pnpm](https://pnpm.io) for every new projects but some legacy project can use [npm](https://www.npmjs.com/) or [yarn](https://classic.yarnpkg.com/). We highly recommend you install [ni](https://github.com/antfu/ni) so you don't worry about the package manager when switching across different projects.

We will use ni's commands in the following code snippets. If you are not using it, you can do the conversion yourself: `ni = pnpm install`, `nr = pnpm run`.

To set the repository up:

| Step                                           | Command              |
|------------------------------------------------|----------------------|
| 1. Install Node.js, using the latest LTS       | -                    |
| 2. Enable Corepack                             | `corepack enable`    |
| 3. Install @antfu/ni                           | `npm i -g @antfu/ni` |
| 4. Install dependencies under the project root | `ni`                 |

## 💡 Commands

Each project can have differents commands depending of the architecture. Please refer to the local `package.json` file.

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
