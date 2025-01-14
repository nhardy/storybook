# Storybook for SvelteKit <!-- omit in toc -->

Our goal is to help you use the tools you love together with Storybook. That’s why Storybook has zero-config support for SvelteKit with the `@storybook/sveltekit` package.

Check out our [Frameworks API](https://storybook.js.org/blog/framework-api/) announcement for what this all means for you and our continued efforts to make Storybook a seamless integration for any project.

## Table of Contents <!-- omit in toc -->

- [Supported features](#supported-features)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
  - [In a project without Storybook](#in-a-project-without-storybook)
  - [In a project with Storybook](#in-a-project-with-storybook)
    - [Automatic migration](#automatic-migration)
    - [Manual migration](#manual-migration)
- [Acknowledgements](#acknowledgements)

## Supported features

All Svelte language features are supported out of the box, as Storybook uses the Svelte compiler underneath.
However SvelteKit has some [Kit-specific modules](https://kit.svelte.dev/docs/modules) that currently aren't supported. It's on our roadmap to support most of them soon:

| **Module**                                                                         | **Status**                                                                                                             |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| [`$app/environment`](https://kit.svelte.dev/docs/modules#$app-environment)         | 🔜 Coming in 7.0                                                                                                       |
| [`$app/forms`](https://kit.svelte.dev/docs/modules#$app-forms)                     | ⏳ Planned for 7.1                                                                                                     |
| [`$app/navigation`](https://kit.svelte.dev/docs/modules#$app-navigation)           | ⏳ Planned for 7.1. With mocks so the Actions addon will display when the hooks are being called.                      |
| [`$app/paths`](https://kit.svelte.dev/docs/modules#$app-paths)                     | 🔜 Coming in 7.0                                                                                                       |
| [`$app/stores`](https://kit.svelte.dev/docs/modules#$app-stores)                   | ⏳ Planned for 7.1. With mocks so you can set different store values per story.                                        |
| [`$env/dynamic/private`](https://kit.svelte.dev/docs/modules#$env-dynamic-private) | ⛔ Not supported. They are meant to only be available server-side, and Storybook renders all components on the client. |
| [`$env/dynamic/public`](https://kit.svelte.dev/docs/modules#$env-dynamic-public)   | 🔜 Coming in 7.0                                                                                                       |
| [`$env/static/private`](https://kit.svelte.dev/docs/modules#$env-static-private)   | ⛔ Not supported. They are meant to only be available server-side, and Storybook renders all components on the client. |
| [`$env/static/public`](https://kit.svelte.dev/docs/modules#$env-static-public)     | 🔜 Coming in 7.0                                                                                                       |
| [`$lib`](https://kit.svelte.dev/docs/modules#$lib)                                 | 🔜 Coming in 7.0                                                                                                       |
| [`$service-worker`](https://kit.svelte.dev/docs/modules#$service-worker)           | ⛔ Not supported. They are only meant to be used in service workers                                                    |
| [`@sveltejs/kit/*`](https://kit.svelte.dev/docs/modules#sveltejs-kit)              | ✅ Supported                                                                                                           |

This is just the beginning. We're planning on making it an even better experience to [build](https://storybook.js.org/docs/7.0/react/writing-stories/introduction), [test](https://storybook.js.org/docs/7.0/react/writing-tests/introduction) and [document](https://storybook.js.org/docs/7.0/react/writing-docs/introduction) all the SvelteKit goodies like [pages](https://kit.svelte.dev/docs/routing), [forms](https://kit.svelte.dev/docs/form-actions) and [layouts](https://kit.svelte.dev/docs/routing#layout) in Storybook, while still integrating with all the addons and workflows you know and love.

## Requirements

- [SvelteKit](https://kit.svelte.dev/) >= 1.0.0 (not including beta versions)
- [Storybook](https://storybook.js.org/) >= 7.x

## Getting Started

### In a project without Storybook

Run the following command in your SvelteKit project's root directory, and follow the prompts:

```bash
npx storybook@next init
```

[More on getting started with Storybook](https://storybook.js.org/docs/7.0/svelte/get-started/install)

### In a project with Storybook

This framework is designed to work with Storybook 7. If you’re not already using v7, upgrade with this command:

```bash
npx storybook@next upgrade --prerelease
```

#### Automatic migration

When running the `upgrade` command above you should get a prompt asking you to migrate to `@storybook/sveltekit`, which should handle everything for you. In some cases it can't migrate for you, eg. if your existing Storybook setup is based on Webpack. In such cases, refer to the manual migration below.

#### Manual migration

Install the framework:

```bash
yarn add -D @storybook/sveltekit@next
```

Update your `main.cjs` to change the framework property:

```js
// .storybook/main.cjs
module.exports = {
  ...
  framework: '@storybook/sveltekit',
};
```

Storybook 7.0 automatically loads your Vite config, and by extension your Svelte config. If you have a `svelteOptions` property in `main.cjs` you should remove that, unless you explicitly want different options between your app and Storybook.

Remove any redundant dependencies, if you have them:

```bash
yarn remove @storybook/svelte-vite
yarn remove @storybook/svelte-webpack5
yarn remove storybook-builder-vite
yarn remove @storybook/builder-vite
```

## Acknowledgements

Integrating with SvelteKit would not have been possible if it weren't for the fantastic efforts by the Svelte core team - especially [Ben McCann](https://twitter.com/benjaminmccann) - to make integrations with the wider ecosystem possible.
