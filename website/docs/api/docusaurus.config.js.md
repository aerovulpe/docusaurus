---
sidebar_position: 0
id: docusaurus.config.js
description: API reference for Docusaurus configuration file.
slug: /api/docusaurus-config
---

# `docusaurus.config.js`

## Overview {#overview}

`docusaurus.config.js` contains configurations for your site and is placed in the root directory of your site.

It usually exports a site configuration object:

```js title="docusaurus.config.js"
module.exports = {
  // site config...
};
```

<details>
<summary>Config files also support config creator functions and async code.</summary>

```js title="docusaurus.config.js"
module.exports = function configCreator() {
  return {
    // site config...
  };
};
```

```js title="docusaurus.config.js"
module.exports = async function configCreatorAsync() {
  return {
    // site config...
  };
};
```

```js title="docusaurus.config.js"
module.exports = Promise.resolve({
  // site config...
});
```

</details>

## Required fields {#required-fields}

### `title` {#title}

- Type: `string`

Title for your website. Will be used in metadata and as browser tab title.

```js title="docusaurus.config.js"
module.exports = {
  title: 'Docusaurus',
};
```

### `url` {#url}

- Type: `string`

URL for your website. This can also be considered the top-level hostname. For example, `https://facebook.github.io` is the URL of https://facebook.github.io/metro/, and `https://docusaurus.io` is the URL for https://docusaurus.io. This field is related to the [baseUrl](#baseurl) field.

```js title="docusaurus.config.js"
module.exports = {
  url: 'https://docusaurus.io',
};
```

### `baseUrl` {#baseUrl}

- Type: `string`

Base URL for your site. Can be considered as the path after the host. For example, `/metro/` is the base URL of https://facebook.github.io/metro/. For URLs that have no path, the baseUrl should be set to `/`. This field is related to the [url](#url) field. Always has both leading and trailing slash.

```js title="docusaurus.config.js"
module.exports = {
  baseUrl: '/',
};
```

## Optional fields {#optional-fields}

### `favicon` {#favicon}

- Type: `string | undefined`

Path to your site favicon; must be a URL that can be used in link's href. For example, if your favicon is in `static/img/favicon.ico`:

```js title="docusaurus.config.js"
module.exports = {
  favicon: '/img/favicon.ico',
};
```

### `trailingSlash` {#trailingSlash}

- Type: `boolean | undefined`

Allow to customize the presence/absence of a trailing slash at the end of URLs/links, and how static HTML files are generated:

- `undefined` (default): keeps URLs untouched, and emit `/docs/myDoc/index.html` for `/docs/myDoc.md`
- `true`: add trailing slashes to URLs/links, and emit `/docs/myDoc/index.html` for `/docs/myDoc.md`
- `false`: remove trailing slashes from URLs/links, and emit `/docs/myDoc.html` for `/docs/myDoc.md`

:::tip

Each static hosting provider serves static files differently (this behavior may even change over time).

Refer to the [deployment guide](../deployment.mdx) and [slorber/trailing-slash-guide](https://github.com/slorber/trailing-slash-guide) to choose the appropriate setting.

:::

### `i18n` {#i18n}

- Type: `Object`

The i18n configuration object to [localize your site](../i18n/i18n-introduction.md).

Example:

<!-- cSpell:ignore فارسی -->

```js title="docusaurus.config.js"
module.exports = {
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'fr'],
    localeConfigs: {
      en: {
        label: 'English',
        direction: 'ltr',
        htmlLang: 'en-US',
        calendar: 'gregory',
      },
      fa: {
        label: 'فارسی',
        direction: 'rtl',
        htmlLang: 'fa-IR',
        calendar: 'persian',
      },
    },
  },
};
```

- `defaultLocale`: The locale that (1) does not have its name in the base URL (2) gets started with `docusaurus start` without `--locale` option (3) will be used for the `<link hrefLang="x-default">` tag
- `locales`: List of locales deployed on your site. Must contain `defaultLocale`.
- `localeConfigs`: Individual options for each locale.
  - `label`: The label displayed for this locale in the locales dropdown.
  - `direction`: `ltr` (default) or `rtl` (for [right-to-left languages](https://developer.mozilla.org/en-US/docs/Glossary/rtl) like Arabic, Hebrew, etc.). Used to select the locale's CSS and html meta attribute.
  - `htmlLang`: BCP 47 language tag to use in `<html lang="...">` and in `<link ... hreflang="...">`
  - `calendar`: the [calendar](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Locale/calendar) used to calculate the date era. Note that it doesn't control the actual string displayed: `MM/DD/YYYY` and `DD/MM/YYYY` are both `gregory`. To choose the format (`DD/MM/YYYY` or `MM/DD/YYYY`), set your locale name to `en-GB` or `en-US` (`en` means `en-US`).

### `noIndex` {#noIndex}

- Type: `boolean`

This option adds `<meta name="robots" content="noindex, nofollow">` to every page to tell search engines to avoid indexing your site (more information [here](https://moz.com/learn/seo/robots-meta-directives)).

Example:

```js title="docusaurus.config.js"
module.exports = {
  noIndex: true, // Defaults to `false`
};
```

### `onBrokenLinks` {#onBrokenLinks}

- Type: `'ignore' | 'log' | 'warn' | 'error' | 'throw'`

The behavior of Docusaurus when it detects any broken link.

By default, it throws an error, to ensure you never ship any broken link, but you can lower this security if needed.

:::note

The broken links detection is only available for a production build (`docusaurus build`).

:::

### `onBrokenMarkdownLinks` {#onBrokenMarkdownLinks}

- Type: `'ignore' | 'log' | 'warn' | 'error' | 'throw'`

The behavior of Docusaurus when it detects any broken markdown link.

By default, it prints a warning, to let you know about your broken markdown link, but you can change this security if needed.

### `onDuplicateRoutes` {#onDuplicateRoutes}

- Type: `'ignore' | 'log' | 'warn' | 'error' | 'throw'`

The behavior of Docusaurus when it detects any [duplicate routes](/guides/creating-pages.md#duplicate-routes).

By default, it displays a warning after you run `yarn start` or `yarn build`.

### `tagline` {#tagline}

- Type: `string`

The tagline for your website.

```js title="docusaurus.config.js"
module.exports = {
  tagline:
    'Docusaurus makes it easy to maintain Open Source documentation websites.',
};
```

### `organizationName` {#organizationName}

- Type: `string`

The GitHub user or organization that owns the repository. You don't need this if you are not using the `docusaurus deploy` command.

```js title="docusaurus.config.js"
module.exports = {
  // Docusaurus' organization is facebook
  organizationName: 'facebook',
};
```

### `projectName` {#projectName}

- Type: `string`

The name of the GitHub repository. You don't need this if you are not using the `docusaurus deploy` command.

```js title="docusaurus.config.js"
module.exports = {
  projectName: 'docusaurus',
};
```

### `deploymentBranch` {#deploymentBranch}

- Type: `string`

The name of the branch to deploy the static files to. You don't need this if you are not using the `docusaurus deploy` command.

```js title="docusaurus.config.js"
module.exports = {
  deploymentBranch: 'gh-pages',
};
```

### `githubHost` {#githubHost}

- Type: `string`

The hostname of your server. Useful if you are using GitHub Enterprise. You don't need this if you are not using the `docusaurus deploy` command.

```js title="docusaurus.config.js"
module.exports = {
  githubHost: 'github.com',
};
```

### `githubPort` {#githubPort}

- Type: `string`

The port of your server. Useful if you are using GitHub Enterprise. You don't need this if you are not using the `docusaurus deploy` command.

```js title="docusaurus.config.js"
module.exports = {
  githubPort: '22',
};
```

### `themeConfig` {#themeConfig}

- Type: `Object`

The [theme configuration](./themes/theme-configuration.md) object to customize your site UI like navbar and footer.

Example:

```js title="docusaurus.config.js"
module.exports = {
  themeConfig: {
    hideableSidebar: false,
    autoCollapseSidebarCategories: false,
    colorMode: {
      defaultMode: 'light',
      disableSwitch: false,
      respectPrefersColorScheme: true,
    },
    navbar: {
      title: 'Site Title',
      logo: {
        alt: 'Site Logo',
        src: 'img/logo.svg',
        width: 32,
        height: 32,
      },
      items: [
        {
          to: 'docs/docusaurus.config.js',
          activeBasePath: 'docs',
          label: 'docusaurus.config.js',
          position: 'left',
        },
        // ... other links
      ],
    },
    footer: {
      style: 'dark',
      links: [
        {
          title: 'Docs',
          items: [
            {
              label: 'Docs',
              to: 'docs/doc1',
            },
          ],
        },
        // ... other links
      ],
      logo: {
        alt: 'Facebook Open Source Logo',
        src: 'https://docusaurus.io/img/oss_logo.png',
        width: 160,
        height: 51,
      },
      copyright: `Copyright © ${new Date().getFullYear()} Facebook, Inc.`, // You can also put own HTML here
    },
  },
};
```

### `plugins` {#plugins}

- Type: `PluginConfig[]`

```ts
type PluginConfig = string | [string, any] | PluginModule | [PluginModule, any];
```

See [plugin method references](./plugin-methods/README.md) for the shape of a `PluginModule`.

```js title="docusaurus.config.js"
module.exports = {
  plugins: [
    'docusaurus-plugin-awesome',
    ['docusuarus-plugin-confetti', {fancy: false}],
    () => ({
      postBuild() {
        console.log('Build finished');
      },
    }),
  ],
};
```

### `themes` {#themes}

- Type: `PluginConfig[]`

```js title="docusaurus.config.js"
module.exports = {
  themes: ['@docusaurus/theme-classic'],
};
```

### `presets` {#presets}

- Type: `PresetConfig[]`

```ts
type PresetConfig = string | [string, any];
```

```js title="docusaurus.config.js"
module.exports = {
  presets: [],
};
```

### `customFields` {#customfields}

Docusaurus guards `docusaurus.config.js` from unknown fields. To add a custom field, define it on `customFields`.

- Type: `Object`

```js title="docusaurus.config.js"
module.exports = {
  customFields: {
    admin: 'endi',
    superman: 'lol',
  },
};
```

Attempting to add unknown fields in the config will lead to errors during build time:

```bash
Error: The field(s) 'foo', 'bar' are not recognized in docusaurus.config.js
```

### `staticDirectories` {#staticDirectories}

An array of paths, relative to the site's directory or absolute. Files under these paths will be copied to the build output as-is.

- Type: `string[]`

Example:

```js title="docusaurus.config.js"
module.exports = {
  staticDirectories: ['static'],
};
```

### `scripts` {#scripts}

An array of scripts to load. The values can be either strings or plain objects of attribute-value maps. The `<script>` tags will be inserted in the HTML `<head>`.

Note that `<script>` added here are render-blocking, so you might want to add `async: true`/`defer: true` to the objects.

- Type: `(string | Object)[]`

Example:

```js title="docusaurus.config.js"
module.exports = {
  scripts: [
    // String format.
    'https://docusaurus.io/script.js',
    // Object format.
    {
      src: 'https://cdnjs.cloudflare.com/ajax/libs/clipboard.js/2.0.0/clipboard.min.js',
      async: true,
    },
  ],
};
```

### `stylesheets` {#stylesheets}

An array of CSS sources to load. The values can be either strings or plain objects of attribute-value maps. The `<link>` tags will be inserted in the HTML `<head>`.

- Type: `(string | Object)[]`

Example:

```js title="docusaurus.config.js"
module.exports = {
  stylesheets: [
    // String format.
    'https://docusaurus.io/style.css',
    // Object format.
    {
      href: 'http://mydomain.com/style.css',
    },
  ],
};
```

### `clientModules` {#clientModules}

An array of [client modules](../advanced/client.md#client-modules) to load globally on your site.

Example:

```js title="docusaurus.config.js"
module.exports = {
  clientModules: [
    require.resolve('./mySiteGlobalJs.js'),
    require.resolve('./mySiteGlobalCss.css'),
  ],
};
```

### `ssrTemplate` {#ssrTemplate}

An HTML template written in [Eta's syntax](https://eta.js.org/docs/syntax#syntax-overview) that will be used to render your application. This can be used to set custom attributes on the `body` tags, additional `meta` tags, customize the `viewport`, etc. Please note that Docusaurus will rely on the template to be correctly structured in order to function properly, once you do customize it, you will have to make sure that your template is compliant with the requirements from upstream.

- Type: `string`

Example:

```js title="docusaurus.config.js"
module.exports = {
  ssrTemplate: `<!DOCTYPE html>
<html <%~ it.htmlAttributes %>>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="generator" content="Docusaurus v<%= it.version %>">
    <% if (it.noIndex) { %>
      <meta name="robots" content="noindex, nofollow" />
    <% } %>
    <%~ it.headTags %>
    <% it.metaAttributes.forEach((metaAttribute) => { %>
      <%~ metaAttribute %>
    <% }); %>
    <% it.stylesheets.forEach((stylesheet) => { %>
      <link rel="stylesheet" href="<%= it.baseUrl %><%= stylesheet %>" />
    <% }); %>
    <% it.scripts.forEach((script) => { %>
      <link rel="preload" href="<%= it.baseUrl %><%= script %>" as="script">
    <% }); %>
  </head>
  <body <%~ it.bodyAttributes %>>
    <%~ it.preBodyTags %>
    <div id="__docusaurus">
      <%~ it.appHtml %>
    </div>
    <% it.scripts.forEach((script) => { %>
      <script src="<%= it.baseUrl %><%= script %>"></script>
    <% }); %>
    <%~ it.postBodyTags %>
  </body>
</html>`,
};
```

### `titleDelimiter` {#titleDelimiter}

- Type: `string`

Will be used as title delimiter in the generated `<title>` tag.

Example:

```js title="docusaurus.config.js"
module.exports = {
  titleDelimiter: '🦖', // Defaults to `|`
};
```

### `baseUrlIssueBanner` {#baseurlIssueBanner}

- Type: `boolean`

When enabled, will show a banner in case your site can't load its CSS or JavaScript files, which is a very common issue, often related to a wrong `baseUrl` in site config.

Example:

```js title="docusaurus.config.js"
module.exports = {
  baseUrlIssueBanner: true, // Defaults to `true`
};
```

![baseUrlIssueBanner](/img/baseUrlIssueBanner.png)

:::caution

This banner needs to inline CSS / JS in case all asset loading fails due to wrong base URL.

If you have a strict [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP), you should rather disable it.

:::
