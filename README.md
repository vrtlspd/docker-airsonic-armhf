[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/airsonic/airsonic
[hub]: https://hub.docker.com/r/lsioarmhf/airsonic/


[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png?v=4&s=4000)][linuxserverurl]


## Contact information:- 

| Type | Address/Details | 
| :---: | --- |
| Discord | [Discord](https://discord.gg/YWrKVTn) |
| Forum | [Linuserver.io forum][forumurl] |
| IRC | freenode at `#linuxserver.io` more information at:- [IRC][ircurl]
| Podcast | Covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation! [Linuxserver.io Podcast][podcasturl] |


The [LinuxServer.io][linuxserverurl] team brings you another image release featuring :-

 + regular and timely application updates
 + easy user mappings
 + custom base image with s6 overlay
 + weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
 + security updates

# lsioarmhf/airsonic
[![](https://images.microbadger.com/badges/version/lsioarmhf/airsonic.svg)](https://microbadger.com/images/lsioarmhf/airsonic "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/airsonic.svg)](https://microbadger.com/images/lsioarmhf/airsonic "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/airsonic.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/airsonic.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-airsonic)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-airsonic/)

Airsonic is a free, web-based media streamer, providing ubiquitious access to your music. Use it to share your music with friends, or to listen to your own music while at work. You can stream to multiple players simultaneously, for instance to one player in your kitchen and another in your living room.

[![airsonic](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/libresonic.png)][appurl]

&nbsp;

## Usage

```
docker create \
--name=airsonic \
-v </path/to/config>:/config \
-v </path/to/music>:/music \
-v </path/to/playlists>:/playlists \
-v </path/to/podcasts>:/podcasts \
-v </path/to/other media>:/media \
-e PGID=<gid> -e PUID=<uid> \
-e CONTEXT_PATH=<url-base> \
-e JAVA_OPTS=<options> \
-e TZ=<timezone> \
-p 4040:4040 \
lsioarmhf/airsonic

```

&nbsp;

## Parameters

The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.



| Parameter | Function |
| :---: | --- |
| `-p 4040` | the port(s) |
| `-v /config` | Configuration file location |
| `-v /music` | Location of music. |
| `-v /playlists` | Location for playlists to be saved to. |
| `-v /podcasts` | Location of podcasts. |
| `-v /media` | Location of other media - *optional* |
| `-e PUID` | for UserID, see below for explanation |
| `-e GUID` | for GroupID, see below for explanation |
| `-e CONTEXT_PATH` | for setting url-base in reverse proxy setups - *optional* |
| `-e JAVA_OPTS` | for passing additional java options - *optional* |
| `-e TZ` | for setting timezone information, eg Europe/London |

&nbsp;

## User / Group Identifiers

Sometimes when using volumes (`-v` flags) permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and it will "just work" &trade;.

In this instance `PUID=1001` and `PGID=1001`, to find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

&nbsp;

## Setting up the application
`IMPORTANT... THIS IS THE ARMF VERSION`

Access WebUI at `<your-ip>:4040`.

Default user/pass is admin/admin

Extra java options can be passed with the JAVA_OPTS environment variable, eg `-e JAVA_OPTS="-Xmx256m -Xms256m"`

&nbsp;

## Container access and information.

| Function | Command |
| :--- | :--- |
| Shell access (live container) | `docker exec -it airsonic /bin/bash` |
| Realtime container logs | `docker logs -f airsonic` |
| Container version number | `docker inspect -f '{{ index .Config.Labels "build_version" }}' airsonic` |
| Image version number |  `docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/airsonic` |

&nbsp;

## Versions

|  Date | Changes |
| :---: | --- |
| 22.04.18 |  Add the forgotten JAVA_OPTS to the run command. |
| 29.12.17 |  Initial Release. |
