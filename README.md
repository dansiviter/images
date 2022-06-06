# Images #

This repository holds common images used in my experiments.

* APKO - Images using the [APKO](/chainguard-dev/apko) image utility
  * `ghcr.io/dansiviter/alpine:3.16-base` - `busybox` and `alpine-baselayout` only base image,
  * `ghcr.io/dansiviter/alpine:3.16-musl` - `musl` only base image,
  * `ghcr.io/dansiviter/alpine:3.16-jlink` - A base image suitable for JLink,
  * `ghcr.io/dansiviter/alpine:3.16-jre17` - A base image suitable for JRE 17,
  * `ghcr.io/dansiviter/alpine:3.16-minirootfs` - Equivilent of the Alpine minirootfs distribution.


## Development ##

To build an image locally, use the following replacing `<filename>` and `<image>:<tag>`:

```powershell
docker run --rm `
  -v $pwd/:/app:rw `
  -w /app `
  ghcr.io/chainguard-dev/apko:v0.3.3 `
  build apko/<filename> <image>:<tag> image.tar
docker load -i image.tar
```


## Sanbox ##

```
jq -r '.components[] | select(.type=="operating-system") | .components[] | select(.name=="openjdk17-jre-headless") | .version' sbom-x86_64.cdx

jq -r '.packages[] | select(.name=="openjdk17-jre-headless") | .versionInfo' sbom-x86_64.spdx.json
```
