[![Chat](https://img.shields.io/matrix/element-web:matrix.org?logo=matrix)](https://matrix.to/#/#element-web:matrix.org)
![Tests](https://github.com/vector-im/element-web/actions/workflows/tests.yaml/badge.svg)
![Static Analysis](https://github.com/vector-im/element-web/actions/workflows/static_analysis.yaml/badge.svg)
[![Weblate](https://translate.element.io/widgets/element-web/-/element-web/svg-badge.svg)](https://translate.element.io/engage/element-web/)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=element-web&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=element-web)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=element-web&metric=coverage)](https://sonarcloud.io/summary/new_code?id=element-web)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=element-web&metric=vulnerabilities)](https://sonarcloud.io/summary/new_code?id=element-web)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=element-web&metric=bugs)](https://sonarcloud.io/summary/new_code?id=element-web)

# Aisland Chat

Aisland Chat is a fork of Element, a Matrix web client built using the [Matrix
React SDK](https://github.com/matrix-org/matrix-react-sdk).

# Supported Environments

Aisland Chat has several tiers of support for different environments:

-   Supported
    -   Definition: Issues **actively triaged**, regressions **block** the release
    -   Last 2 major versions of Chrome, Firefox, and Edge on desktop OSes
    -   Last 2 versions of Safari
    -   Latest release of official Element Desktop app on desktop OSes
    -   Desktop OSes means macOS, Windows, and Linux versions for desktop devices
        that are actively supported by the OS vendor and receive security updates
-   Experimental
    -   Definition: Issues **accepted**, regressions **do not block** the release
    -   Element as an installed PWA via current stable version of Chrome
    -   Mobile web for current stable version of Chrome, Firefox, and Safari on Android, iOS, and iPadOS
-   Not supported
    -   Definition: Issues only affecting unsupported environments are **closed**
    -   Everything else

For accessing Aisland Chat on an Android or iOS device, we currently recommend the
native apps [element-android](https://github.com/vector-im/element-android)
and [element-ios](https://github.com/vector-im/element-ios).

# Getting Started

The easiest way to test Aisland Chat is to just use the hosted copy at <https://chat.aisland.io>.

# Building From Source

Aisland Chat is a modular webapp built with modern ES6 and uses a Node.js build system.
Ensure you have the latest LTS version of Node.js installed.

Using `yarn` instead of `npm` is recommended. Please see the Yarn [install
guide](https://classic.yarnpkg.com/en/docs/install) if you do not have it already.

1. Install or update `node.js` so that your `node` is at least the current recommended LTS.
1. Install `yarn` if not present already.
1. Clone the repo: `git clone https://github.com/vector-im/element-web.git`.
1. Switch to the element-web directory: `cd element-web`.
1. Install the prerequisites: `yarn install`.
    - If you're using the `develop` branch, then it is recommended to set up a
      proper development environment (see [Setting up a dev
      environment](#setting-up-a-dev-environment) below). Alternatively, you
      can use <https://develop.element.io> - the continuous integration release of
      the develop branch.
1. Configure the app by copying `config.sample.json` to `config.json` and
   modifying it. See the [configuration docs](docs/config.md) for details.
1. `yarn dist` to build a tarball to deploy. Untaring this file will give
   a version-specific directory containing all the files that need to go on your
   web server.

Note that `yarn dist` is not supported on Windows, so Windows users can run `yarn build`,
which will build all the necessary files into the `webapp` directory. The version of Element
will not appear in Settings without using the dist script. You can then mount the
`webapp` directory on your web server to actually serve up the app, which is
entirely static content.

# Caching requirements

Aisland Chat requires the following URLs not to be cached, when/if you are serving Aisland chat from your own webserver:

```
/config.*.json
/i18n
/home
/sites
/index.html
```

We also recommend that you force browsers to re-validate any cached copy of Aisland Chat on page load by configuring your
webserver to return `Cache-Control: no-cache` for `/`. This ensures the browser will fetch a new version of Element on
the next page load after it's been deployed. Note that this is already configured for you in the nginx config of our
Dockerfile.

