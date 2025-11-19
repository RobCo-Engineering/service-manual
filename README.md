<div align="center">
  <img 
    align="center" 
    src=".github/images/robco.png" 
    width="250"
  />
  <h1 align="center">RobCo Industries - Service Manual</h1>
  <p align="center">
    Fan built RobCo Industries engineering handbook that documents Pip Boy hardware, troubleshooting, upgrades, and custom firmware.
  </p>
</div>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Index <a name="index"></a>

- [Community](#community)
  - [Websites](#websites)
  - [Discord Servers](#discord-servers)
  - [Related Projects & Source Material](#related-projects-source-material)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Local Development](#local-development)
- [Build](#build)
- [Deployment](#deployment)
- [Info](#info)

## Community <a name="community"></a>

### Websites <a name="websites"></a>

- [RobCo Industries][link-robco-industries]
- [Pip-Boy][link-pip-boy-terminal]
- [The Wand Company][link-the-wand-company]

<!-- If you contribute, self promote here! -->

### Discord Servers <a name="discord-servers"></a>

- [RobCo Industries][link-discord-robco-industries]
- [Pip-Boy][link-discord-pip-boy]

<!-- Might be cool to list *all* Fallout Discords here in the future. -->

### Related Projects & Source Material <a name="related-projects-source-material"></a>

- [Espruino][link-espruino]
- [Pip-Boy][link-pip-boy-repo]
- [Pip-Boy 3000 Mk V - Apps & Games][link-pip-boy-apps]
- [Pip-Boy 3000 Mk V - Media Converter][link-pip-boy-media-converter]

<!-- Add any referenced source material here -->

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Prerequisites <a name="prerequisites"></a>

- [Node.js](https://nodejs.org/)

- Yarn

```bash
npm install --global yarn
```

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Installation <a name="installation"></a>

Build fresh packages.

```bash
yarn
```

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Local Development <a name="local-development"></a>

```bash
yarn start
```

This command starts a local development server and opens up a browser window.
Most changes are reflected live without having to restart the server.

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Build <a name="build"></a>

```bash
yarn build
```

This command generates static content into the `build` directory and can be
served using any static contents hosting service.

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Deployment <a name="deployment"></a>

````bash

Using SSH:

```bash
USE_SSH=true yarn deploy
````

Not using SSH:

```bash
GIT_USER=<Your GitHub username> yarn deploy
```

If you are using GitHub pages for hosting, this command is a convenient way to
build the website and push to the `gh-pages` branch.

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Info <a name="info"></a>

This website is built using [Docusaurus](https://docusaurus.io/), a modern
static website generator.

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

<!-- LINK REFERENCES -->

[link-discord-pip-boy]: https://discord.gg/zQmAkEg8XG
[link-discord-robco-industries]: https://discord.gg/WNEuWsck6n
[link-espruino]: https://github.com/espruino/Espruino
[link-pip-boy-apps]: https://github.com/CodyTolene/pip-boy-apps
[link-pip-boy-media-converter]:
  https://github.com/CodyTolene/pip-boy-3000-mk-v-media-converter
[link-pip-boy-repo]: https://github.com/CodyTolene/pip-terminal
[link-pip-boy-terminal]: https://pip-boy.com/
[link-robco-industries]: https://log.robco-industries.org/
[link-the-wand-company]: https://www.thewandcompany.com/
