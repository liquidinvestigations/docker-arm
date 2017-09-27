Scripts to build docker images on ARM. They clone the upstream repo, run Docker
with a custom Dockerfile, and save the images to `/mnt/shared/docker-images`.

### Usage
```
./build hoover-ui
./build hoover-snoop
./build hoover-search
```
