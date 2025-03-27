# Web Deploy, Deployer of Web

This is a simple script to auto-deploy new instances on my personal website
using `systemd`.

## Usage

Dependencies:

- git
- systemd

Clone and run the initializer.

> `sudo` is required to move the files to their appropriate locations. See the
> [init](#init) section for more info.

```bash
git clone https://github.com/jtriley2p/deployer-of-web && \
    cd web-deploy && \
    ./init
```

## Relevant Files

### [init](./init)

Initializer, it sends each file to their appropriate place.

- `web-deploy` -> `/usr/local/bin/web-deploy`
- `web-deploy.service` -> `/etc/systemd/system/web-deploy.service`
- `web-deploy.timer` -> `/etc/systemd/system/web-deploy.timer`

### [web-deploy](./web-deploy)

Deployer of web.

Checks if there are any changes on the remote, if so, it pulls the latest from
github, runs a backup of the current website, deploys the new website.

Relevant paths:

- `/var/www/jtriley.com/public/`: website directory
- `/var/cache/web-deployer/jtriley-com/`: cached repository directory
  - `./src/`: html source directory
- `/var/cache/web-deployer/jtriley-com-backup/`: backup directory

### [web-deploy.service](./web-deploy.service)

Systemd service unit. Runs the script as the root user.

### [web-deploy.timer](./web-deploy.timer)

Systemd timer unit, runs the [web-deploy.service](./web-deploy.service)
service unit on a designated timescale.
