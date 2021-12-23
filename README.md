Alpine Python and GNU C library (glibc) Docker image
=========================================

This image is based on a combination of the official python Alpine Linux image,
which is only a 45MB image, and [frolvlad/alpine-glibc](https://github.com/Docker-Hub-frolvlad/docker-alpine-glibc). 
glibc is included to enable proprietary projects compiled against glibc
(e.g. OracleJDK, Anaconda) rather than alpine's default musl.

It will come in around 58MB, which is somthing of a happy medium between vanilla
alpine and the slightly larger debian-based python images.

This image includes some quirks to make [glibc](https://www.gnu.org/software/libc/) work side by
side with musl libc (default in Alpine Linux). glibc packages
for Alpine Linux are prepared by
[Sasha Gerrand](https://github.com/sgerrand) and the releases are published in
[sgerrand/alpine-pkg-glibc](https://github.com/sgerrand/alpine-pkg-glibc) github repo.

If you need to update your libc library cache, use
`/usr/glibc-compat/sbin/ldconfig` instead of the usual `/sbin/ldconfig`.
You can also use the `LD_LIBRARY_PATH` as on standard libc-based distributions.


Usage Example
-------------

This image is intended to be a base image for your projects, so you may use it like this:

```Dockerfile
[FROM](FROM) revarcline/python-3-alpine-glibc:latest

COPY ./my_app /usr/local/bin/my_app
```

```sh
$ docker build -t my_app .
