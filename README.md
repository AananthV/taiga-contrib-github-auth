Taiga contrib github auth
=========================

[![Kaleidos Project](http://kaleidos.net/static/img/badge.png)](https://github.com/kaleidos "Kaleidos Project")
[![Managed with Taiga.io](https://img.shields.io/badge/managed%20with-TAIGA.io-709f14.svg)](https://tree.taiga.io/project/taiga/ "Managed with Taiga.io")

The Taiga plugin for github authentication.

## Production env

Take the latest release of this repository, for instance:

```
export TAIGA_CONTRIB_GITHUB_AUTH_TAG=6.0.0
```

### Taiga Back

Activate your virtualenv and install this package:

```bash
pip install "git+https://github.com/taigaio/taiga-contrib-github-auth.git@${TAIGA_CONTRIB_GITHUB_AUTH_TAG}#egg=taiga-contrib-github-auth&subdirectory=back"
```

Modify your `settings/config.py` and include the line:

```python
  INSTALLED_APPS += ["taiga_contrib_github_auth"]

  # Get these from https://github.com/settings/developers
  GITHUB_API_CLIENT_ID = "YOUR-GITHUB-CLIENT-ID"
  GITHUB_API_CLIENT_SECRET = "YOUR-GITHUB-CLIENT-SECRET"
```

**Tip** the callback url in the Github configuration should be the same as the `TAIGA_URL` environment variable.

### Taiga Front

Download in your `dist/plugins/` directory of Taiga front the `taiga-contrib-github-auth` compiled code (you need subversion in your system):

```bash
  cd dist/
  mkdir -p plugins
  cd plugins
  svn export "https://github.com/taigaio/taiga-contrib-github-auth/tags/${TAIGA_CONTRIB_GITHUB_AUTH_TAG}/front/dist"  "github-auth"
```

Include in your `dist/conf.json` in the 'contribPlugins' list the value `"/plugins/github-auth/github-auth.json"` and the `gitHubClientId`:

```json
...
    "gitHubClientId": "YOUR-GITHUB-CLIENT-ID",
    "contribPlugins": [
        (...)
        "/plugins/github-auth/github-auth.json"
    ]
...
```

## Dev env

This configuration should be used only if you're developing this library.

### Taiga Back

Clone the repo and

```bash
  cd taiga-contrib-github-auth/back
  workon taiga
  pip install -e .
```

Modify `taiga-back/settings/local.py` and include the line:

```phyton
  INSTALLED_APPS += ["taiga_contrib_github_auth"]

  # Get these from https://github.com/settings/developers
  GITHUB_API_CLIENT_ID = "YOUR-GITHUB-CLIENT-ID"
  GITHUB_API_CLIENT_SECRET = "YOUR-GITHUB-CLIENT-SECRET"
```

### Taiga Front

After clone the repo link `dist` in `taiga-front` plugins directory:

```bash
  cd taiga-front/dist
  mkdir -p plugins
  cd plugins
  ln -s ../../../taiga-contrib-github-auth/front/dist github-auth
```

Include in your `dist/conf.json` in the 'contribPlugins' list the value `"/plugins/github-auth/github-auth.json"` and the `gitHubClientId`:

```json
...
    "gitHubClientId": "YOUR-GITHUB-CLIENT-ID",
    "contribPlugins": [
        (...)
        "/plugins/github-auth/github-auth.json"
    ]
...
```

In the plugin source dir `taiga-contrib-github-auth/front` run

```bash
npm install
```
and use:

- `gulp` to regenerate the source and watch for changes.
- `gulp build` to only regenerate the source.

## Running tests

We only have backend tests, you have to add your `taiga-back` directory to the
PHYTONPATH environment variable, and run py.test, for example:

```bash
  cd back
  add2virtualenv /home/taiga/taiga-back/
  py.test
```

## Documentation

Currently, we have authored three main documentation hubs:

- **[API](https://taigaio.github.io/taiga-doc/dist/api.html)**: Our API documentation and reference for developing from Taiga API.
- **[Documentation](https://taigaio.github.io/taiga-doc/dist/)**: If you need to install Taiga on your own server, this is the place to find some guides.
- **[Taiga Resources](https://resources.taiga.io)**: This page is intended to be the support reference page for the users.

## Bug reports

If you **find a bug** in Taiga you can always report it:

- in [Taiga issues](https://tree.taiga.io/project/taiga/issues). **This is the preferred way**
- in [Github issues](https://github.com/taigaio/taiga-contrib-github-auth/issues)
- send us a mail to support@taiga.io if is a bug related to [tree.taiga.io](https://tree.taiga.io)
- send us a mail to security@taiga.io if is a **security bug**

One of our fellow Taiga developers will search, find and hunt it as soon as possible.

Please, before reporting a bug, write down how can we reproduce it, your operating system, your browser and version, and if it's possible, a screenshot. Sometimes it takes less time to fix a bug if the developer knows how to find it.

## Community

If you **need help to setup Taiga**, want to **talk about some cool enhancemnt** or you have **some questions**, please write us to our [mailing list](https://groups.google.com/d/forum/taigaio).

If you want to be up to date about announcements of releases, important changes and so on, you can subscribe to our newsletter (you will find it by scrolling down at [https://taiga.io](https://www.taiga.io/)) and follow [@taigaio](https://twitter.com/taigaio) on Twitter.

## Contribute to Taiga

There are many different ways to contribute to Taiga's platform, from patches, to documentation and UI enhancements, just find the one that best fits with your skills. Check out our detailed [contribution guide](https://resources.taiga.io/extend/how-can-i-contribute/)

## Code of Conduct

Help us keep the Taiga Community open and inclusive. Please read and follow our [Code of Conduct](https://github.com/taigaio/code-of-conduct/blob/master/CODE_OF_CONDUCT.md).

## License

Every code patch accepted in Taiga codebase is licensed under [AGPL v3.0](http://www.gnu.org/licenses/agpl-3.0.html). You must be careful to not include any code that can not be licensed under this license.

Please read carefully [our license](https://github.com/taigaio/taiga-contrib-github-auth/blob/master/LICENSE) and ask us if you have any questions as well as the [Contribution policy](https://github.com/taigaio/taiga-contrib-github-auth/blob/master/CONTRIBUTING.md).
