# Notes
Images are [stored](https://wiki.archlinux.org/index.php/Docker#Images_location) by default in `/var/lib/docker`, but you can change the partition and specify the path of the new mounted partition in the `/etc/docker/daemon.json` file, under the `data-root` entry.

**definition containers:** filesystem within a filesystem: an isolated filesystem accessible from a host computer; similar to VMs but containing only essential information, ligthweigth and developed to only perform this specific task and containers they share the kernel with the host. Use one container for a single specific task, so you have only limited list of software in a container, it is more modular.

**base vs non base images:** the first are highly reliable and very well maintained, but the latter are not. They are on dockerhub because in academic settings people do not want to pay for the service and post everything in public mode.

**layers:** users install new software from base image, and docker stores new installations in a new layer. Efficiency and easy because you do not need to rebuild everything.

**deamon:** docker commands are an API to a deamon and that can be annoiying in HPC for instance. Singularity no deamon, permissions of the user in the host are the same as in the container. You can convert from docker to singularity, but you loose the layer organization. Singularity mounts all the directory in your working directory, in docker you need to mount them.

**docker commit not reproducible:** 1. because to rebuild the image you need to whole image (1GB) 2. problem with software versions 3. exact build steps are not described by default

**docker engine:** 1. socket 2. service 3. docker 

**images:** saved on your computer and do not change, takes place `docker save`

**share:** dockerhub image is not very good because it's hard to recreate, it is better to share the dockerfile on git repo and store the image with a link dockerhub.

**dead issue:** some containers wont work because some , use tagged software.

**mounting:** have a look at `volume`, which is better than the default `bind-mount` option. Mounting to create a shared folder between your container and your host. You can also mount read-only. 

**root:** if you are root in the container, you are root in the host too. Specify the user inside the container: `docker run -u "$(id -u):$(id -g)`

**mapping ports:** `docker run -p 80:8000` in the container is `8000` and on the host `80`, so you need to `127.0.0.1:80`

**distroless containers:** very interesting maybe worth studying [here](https://github.com/GoogleContainerTools/distroless#why-should-i-use-distroless-images). Instead of static linking at the distro level, `bazel` statically links at the language level. But for distroless you do not `bazel`, you can do everything from a dockerfile.

**pipelines:** reproducible and deploy everywhere, snakemake.

## Questions

Can we use docker in rootless mode, that is running the deamon without root privileges, or is it better to use singularity?

I [added myself](https://docs.docker.com/engine/install/linux-postinstall/) to the group `docker` to avoid typing `sudo` every time. Is it a good idea / is it safe to do that? 
Yes I think most people running docker on a linux computer have it set up that way. I would have to check, but I’m pretty sure that if you set it up properly the docker group has more limited permissions compared to root, so in that way it’s actually safer to do it in that way.
