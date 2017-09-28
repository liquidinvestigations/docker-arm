Scripts to build docker images on ARM. They clone the upstream repo, run Docker
with a custom Dockerfile, and save the images to `/mnt/shared/docker-images`.

### Usage
Build the images in a
[buildbot](https://github.com/liquidinvestigations/buildbot) VM. `TARGET` is
the path to a docker configuration folder, e.g. `hoover-search`:
```
./build TARGET target.dockers
```

Then, import the images on a machine where docker is logged in to docker hub,
and push them:

```
docker login
./upload target.dockers
```
