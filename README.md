# RPI-Transmission

Transmission docker container

Forked from [dperson/transmission](https://github.com/dperson/transmission/) with
added support for RaspberryPi

# What is Transmission?

Transmission is a BitTorrent client which features a simple interface on top of
a cross-platform back-end.

# How to use this image

## Hosting a Transmission instance

    sudo docker run --name transmission -p 9091:9091 -d scenting/rpi-transmission

OR set local storage:

    sudo docker run --name transmission -p 9091:9091 \
                -v /path/to/directory:/var/lib/transmission-daemon/downloads \
                -d scenting/rpi-transmission

## Configuration

    sudo docker run -it --rm scenting/rpi-transmission -h

    Usage: transmission.sh [-opt] [command]
    Options (fields in '[]' are optional, '<>' are required):
        -h          This help
        -t ""       Configure timezone
                    possible arg: "[timezone]" - zoneinfo timezone for container

    The 'command' (if provided and valid) will be run instead of transmission

ENVIROMENT VARIABLES (only available with `docker run`)

 * `TRUSER` - Set the username for transmission auth (default 'admin')
 * `TRPASSWD` - Set the password for transmission auth (default 'admin')
 * `TZ` - As above, configure the zoneinfo timezone, IE `EST5EDT`
 * `USERID` - Set the UID for the app user
 * `GROUPID` - Set the GID for the app user

## Examples

Any of the commands can be run at creation with `docker run` or later with
`docker exec transmission.sh` (as of version 1.3 of docker).

### Setting the Timezone

    sudo docker run --name transmission -d scenting/rpi-transmission -t EST5EDT

OR using `environment variables`

    sudo docker run --name transmission -e TZ=EST5EDT -d scenting/rpi-transmission

Will get you the same settings as

    sudo docker run --name transmission -p 9091:9091 -d scenting/rpi-transmission
    sudo docker exec transmission transmission.sh -t EST5EDT \
                ls -AlF /etc/localtime
    sudo docker restart transmission

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact me
through a [GitHub issue](https://github.com/scenting/rpi-transmission/issues).
