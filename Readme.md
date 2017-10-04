Scripts to build docker images on ARM and upload them to docker hub.

### Usage
Build the images in a
[factory](https://github.com/liquidinvestigations/factory) VM. `TARGET` is the
path to a docker configuration folder, e.g. `hoover-search`. The second
argument is the path to an output file containing the docker image:

```
./build TARGET target.dockers
```

Then, using a machine where docker is logged into docker hub, import the image
and push it:

```
docker login
./upload target.dockers
```
