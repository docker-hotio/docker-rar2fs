# rar2fs

<img src="https://raw.githubusercontent.com/hotio/docker-rar2fs/master/img/rar2fs.png" alt="Logo" height="130" width="130">

[![GitHub](https://img.shields.io/badge/source-github-lightgrey)](https://github.com/hotio/docker-rar2fs)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/rar2fs)](https://hub.docker.com/r/hotio/rar2fs)
[![Discord](https://img.shields.io/discord/610068305893523457?color=738ad6&label=discord&logo=discord&logoColor=white)](https://discord.gg/3SnkuKp)
[![Upstream](https://img.shields.io/badge/upstream-project-yellow)](https://github.com/hasse69/rar2fs)

## Starting the container

Just the basics to get the container running:

```shell
docker run --rm hotio/rar2fs ...
```

The default `ENTRYPOINT` is `rar2fs -f -o auto_unmount`.

## Tags

| Tag      | Description                    | Build Status                                                                                                                                          | Last Updated                                                                                                                                                  |
| ---------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| latest   | The same as `stable`           |                                                                                                                                                       |                                                                                                                                                               |
| stable   | Stable version                 | [![Build Status](https://cloud.drone.io/api/badges/hotio/docker-rar2fs/status.svg?ref=refs/heads/stable)](https://cloud.drone.io/hotio/docker-rar2fs) | [![GitHub last commit (branch)](https://img.shields.io/github/last-commit/hotio/docker-rar2fs/stable)](https://github.com/hotio/docker-rar2fs/commits/stable) |

You can also find tags that reference a commit or version number.

## Using the rar2fs mount on the host

By setting the `bind-propagation` to `shared` on the volume `mountpoint`, like this `-v /data/mountpoint:/mountpoint:shared`, you are able to access the mount from the host. If you want to use this mount in another container, the best solution is to create a volume on the parent folder of that mount with `bind-propagation` set to `slave`. For example, `-v /data:/data:slave` (`/data` on the host, would contain the previously created volume `mountpoint`). Doing it like this will ensure that when the container creating the mount restarts, the other containers using that mount will recover and keep working.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a rar2fs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```
