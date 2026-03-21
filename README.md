# magento-builder

Docker images for building and deploying Magento 2 projects, extending the official
[Magento Cloud Docker PHP CLI](https://hub.docker.com/r/magento/magento-cloud-docker-php)
images with [Puppeteer](https://pptr.dev/) support for headless browser operations
(e.g. critical CSS generation, automated browser tasks).

Published internally on gitlab-registry.collab.pl and on Docker Hub as [`collabpl/magento-builder`](https://hub.docker.com/r/collabpl/magento-builder).

## Available tags

| Tag | Base image | PHP |
|-----|-----------|-----|
| `8.3` | `magento/magento-cloud-docker-php:8.3-cli-1.4.7` | 8.3 |
| `8.4` | `magento/magento-cloud-docker-php:8.4-cli-1.4.7` | 8.4 |
| `8.5` | `magento/magento-cloud-docker-php:8.5-cli-1.4.7` | 8.5 |

## What's included

On top of the upstream Magento Cloud Docker PHP CLI image, each variant adds:

- System packages required to run Puppeteer / headless Chromium:
  `libnss3`, `libxss1`, `libasound2`, `libatk-bridge2.0-0`, `libgtk-3-0`,
  `libgbm-dev`, `libx11-xcb1`, `libxtst-dev`
- [`puppeteer`](https://www.npmjs.com/package/puppeteer) installed globally via npm

By default all images come with the following PHP extensions:
`bcmath`, `bz2`, `calendar`, `exif`, `gd`, `gettext`, `intl`, `mysqli`, `opcache`,
`pdo_mysql`, `redis`, `soap`, `sockets`, `sodium`, `sysvmsg`, `sysvsem`, `sysvshm`,
`xsl`, `zip`, `pcntl`, `ftp`

## Usage

```bash
docker pull gitlab-registry.collab.pl/collab/docker/magento-builder:8.4
```

```bash
docker run --rm -v $(pwd):/app -w /app gitlab-registry.collab.pl/collab/docker/magento-builder:8.4 bin/magento ...
```

## Repository structure

```
.
├── 8.3/
│   └── Dockerfile
├── 8.4/
│   └── Dockerfile
├── 8.5/
│   └── Dockerfile
├── .github/
│   └── workflows/        # GitHub Actions — build & push to Docker Hub
└── .gitlab-ci.yml        # GitLab CI — build via Kaniko
```

## CI/CD

Images are built and pushed automatically on every push to `main` and on each
published GitHub release.

**GitHub Actions** builds for `linux/amd64` and pushes to Docker Hub using
`DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` repository secrets.

**GitLab CI** uses the internal
[`kaniko-build`](https://gitlab.com/collab/components/kaniko-build) component
to build all three variants in parallel.

## Contributing

1. Edit the relevant `Dockerfile` under the PHP version directory.
2. Push to `main` — CI will rebuild and publish the updated image automatically.
3. To trigger a build manually, use the **workflow_dispatch** trigger in GitHub Actions.

## License

MIT
