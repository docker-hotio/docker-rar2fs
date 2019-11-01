# rar2fs

[![GitHub](https://img.shields.io/badge/source-github-lightgrey?style=flat-square)](https://github.com/hotio/docker-rar2fs)
[![Docker Pulls](https://img.shields.io/docker/pulls/hotio/rar2fs?style=flat-square)](https://hub.docker.com/r/hotio/rar2fs)
[![Drone (cloud)](https://img.shields.io/drone/build/hotio/docker-rar2fs?style=flat-square)](https://cloud.drone.io/hotio/docker-rar2fs)

## Starting the container

Just the basics to get the container running:

```shell
docker run --rm --name rar2fs -v /tmp/input:/input -v /tmp/output:/output:shared -e TZ=Etc/UTC hotio/rar2fs
```

The environment variables below are all optional, the values you see are the defaults.

```shell
-e PUID=1000
-e PGID=1000
-e UMASK=022
-e INPUT_DIR=/input
-e OUTPUT_DIR=/output
```

## Using the rar2fs mount on the host or in another container

By using the option `:shared` on your volume, you'll be able to access the rar2fs mount by going to the folder `/tmp/output` on the host. If you add `--volumes-from rar2fs` to another container's run command, you can go to the rar2fs mount from within that container, by default `/output`.

## Extra docker privileges

In most cases you will need some or all of the following flags added to your command to get the required docker privileges when using a rclone or rar2fs mount.

```shell
--security-opt apparmor:unconfined --cap-add SYS_ADMIN --device /dev/fuse
```

## Executing your own scripts

If you have a need to do additional stuff when the container starts or stops, you can mount your script with `-v /docker/host/my-script.sh:/etc/cont-init.d/99-my-script` to execute your script on container start or `-v /docker/host/my-script.sh:/etc/cont-finish.d/99-my-script` to execute it when the container stops. An example script can be seen below.

```shell
#!/usr/bin/with-contenv bash

echo "Hello, this is me, your script."
```
