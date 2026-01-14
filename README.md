# DOCKER FIRST AID KIT

[![license](https://img.shields.io/badge/license-BSD-3)](LICENSE.md) [![Donate](https://img.shields.io/badge/GUMROAD-36a9ae?style=flat&logo=gumroad&logoColor=white)](https://mcandre.gumroad.com/)

# ABOUT

We provide practical guidance here, for making the best use of the amazing Docker containerized application system.

## GENERAL

# What the heck is Docker?

Docker works like tupperware for software applications.

Docker is a system for bundling, transferring, and enjoying software applications. Docker is an implementation of the more general idea of application *containers*, based on the `cgroups` functionality of the Linux kernel.

Before Docker, engineers used older tools like Vagrant and virtual machines, in order to accomplish similar goals. But virtual machines are less efficient than containers.

Many digital systems continue to run as host-native applications; they never adopted containerization (or virtualization). For these legacy style applications, migrating to Docker can dramatically improve reliability.

Looking past Docker into the future, High Performance Computing (HPC) alternatives include FPGA's and serverless computing. These disciplines are helpful in the pursuit of hyperoptimization, when the cost of engineering is outweighed by intense needs for realtime programming, low latency programming, or reducing cloud computing fees to the absolute minimum. However, HPC tech tends to restrict functionality compared to general purpose containers. HPC is also a moving target at a technical level, where the tools involved can change quite rapidly.

Fortuantely, containers provide a convenient middle ground between the extremes of host-native applications and HPC applications. The practice of containers is relatively easy to adopt, and suitably *impactful*. The current state of the art in Internet scale deployments relies heavily on Docker containers.

# Avoid daemons

For Dockerfile `COMMAND`s and `ENTRYPOINT`s, avoid launching processes as background daemons. Daemons trigger Docker to artificially terminate containers early, because Docker drives the entire container system using direct, foreground user application processes.

For example, avoid using init scripts/services, which are normally designed for use in backgrounded, traditional host contexts.

## Avoid docker-compose

`docker-compose` is a vistigial tool for gluing containers together into an aggregate application. `docker-compose` is ill-suited for production use.

Today, we enjoy much better tools for this, such as `minikube`. In fact, `minikube` replicates production Kubernetes environments much more closely than `docker-compose`. This helps to bridge the developer / operator gap at many technical organizations.

## Configuration

### Guests

For guest base layers, prefer `scratch`, a GNU/Linux flavor, or a musl/Linux flavor. While other guest operating systems are available such as Windows, FreeBSD, etc., these tend to restrict the kinds of different host machines able to run your containers.

Optimal attack surface:

* scratch

Optimal image size:

* scratch
* Alpine Linux
* Debian or Ubuntu

Optimal portability:

* scratch
* Debian or Ubuntu
* Fedora

## Hosts

For host operating system, prefer a Kubernetes node, a GNU/Linux flavor, a musl/Linux flavor, macOS, or Windows. While other host operating systems are available such as Alpine Linux, OpenWrt, Void Linux, FreeBSD, etc., these tend to restrict the kinds of guest containers able to run on different hosts.

Optimal support for assorted guest containers:

* macOS
* Windows
* GNU/Linux

### Docker resource allocation

Reserve >= 256 GB space on the host for Docker resources. Reserve >= 1 TB on CI/CD hosts.

This ensures smoother operation, such as when using Docker for multiple software projects.

For laptops, ensure the host is actively receiving power from a wall outlet. This helps the CPU to run at a faster clock rate.

Quit any other resource-intensive applications that may be running. This helps to reduce interruption to container processes.

Set `CPUs` to the number of (efficiency) cores. This allows Docker to use more of the available host CPU resources.

Set `Memory` to 8 GB or higher. This allows Docker to use more of the available host RAM resources.

Set `Swap` to 1 GB or higher. This allows Docker to use more host resources for swap space.

Set `Virtual disk limit` to 128 GB or higher. This allows Docker to use more of the available host file system resources, particularly for guest /tmp operations.

# VARIOUS DOCKER FAILURES

Docker may begin to act strangely after resuming from host hibernation. When in doubt, restart the Docker service.

# CLEAN

Regularly remove stale containers listed in `docker ps -a`. This removes junk from CPU and disk.

Regularly remove stale images listed in `docker images`. This removes junk from the local Docker image registry.

Regularly run `docker system prune -f`. This often removes an enormous amount of Docker temporary data.

# RESOURCES

* [Docker](https://www.docker.com/)
* [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file)
* [Docker Multi-stage builds](https://docs.docker.com/build/building/multi-stage/)
* [Docker Hub](https://hub.docker.com/)
* [Flatpak](https://flatpak.org/)
* [FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array)
* [Go](https://go.dev/)
* [Kubernetes](https://kubernetes.io/)
* [minikube](https://minikube.sigs.k8s.io/docs/start/)
* [Serverless computing](https://en.wikipedia.org/wiki/Serverless_computing)
* [tuggy](https://github.com/mcandre/tuggy)
