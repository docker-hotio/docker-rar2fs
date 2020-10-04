[<img src="https://hotio.dev/img/rar2fs.png" alt="logo" height="130" width="130">](https://github.com/hasse69/rar2fs)

[![GitHub Source](https://img.shields.io/badge/github-source-ffb64c?style=flat-square&logo=github&logoColor=white)](https://github.com/docker-hotio/docker-rar2fs)
[![GitHub Registry](https://img.shields.io/badge/github-registry-ffb64c?style=flat-square&logo=github&logoColor=white)](https://github.com/users/hotio/packages/container/package/rar2fs)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/rar2fs?color=ffb64c&style=flat-square&label=pulls&logo=docker&logoColor=white)](https://hub.docker.com/r/hotio/rar2fs)
[![Discord](https://img.shields.io/discord/610068305893523457?style=flat-square&color=ffb64c&label=discord&logo=discord&logoColor=white)](https://hotio.dev/discord)
[![Upstream](https://img.shields.io/badge/upstream-project-ffb64c?style=flat-square)](https://github.com/hasse69/rar2fs)
[![Website](https://img.shields.io/badge/website-hotio.dev-ffb64c?style=flat-square)](https://hotio.dev/containers/rar2fs)

## Starting the container

Just the basics to get the container running:

```shell
docker run --rm hotio/rar2fs ...
```

The default `ENTRYPOINT` is `rar2fs -f -o auto_unmount`.

## Tags

| Tag                | Upstream        | Version |
| -------------------|-----------------|---------|
| `release` (latest) | GitHub releases | ![version](https://img.shields.io/badge/dynamic/json?color=f5f5f5&style=flat-square&label=&query=%24.version&url=https%3A%2F%2Fraw.githubusercontent.com%2Fdocker-hotio%2Fdocker-rar2fs%2Frelease%2FVERSION.json) |

You can also find tags that reference a commit or version number.

## Using the rar2fs mount on the host

By setting the `bind-propagation` to `shared` on the volume `mountpoint`, like this `-v /data/mountpoint:/mountpoint:shared`, you are able to access the mount from the host. If you want to use this mount in another container, the best solution is to create a volume on the parent folder of that mount with `bind-propagation` set to `slave`. For example, `-v /data:/data:slave` (`/data` on the host, would contain the previously created volume `mountpoint`). Doing it like this will ensure that when the container creating the mount restarts, the other containers using that mount will recover and keep working.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a rar2fs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```
