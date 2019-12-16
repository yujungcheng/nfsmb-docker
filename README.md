[![Docker Build](https://img.shields.io/docker/build/inwinstack/nfsmb-docker.svg)](https://hub.docker.com/r/inwinstack/nfsmb-docker/)
# NFS & SAMBA Docker Tool-kit
Docker image to run NFS and SAMBA service.

### Build Tool-kit sub-commands
In NFS&SAMBA Docker Tool-kit directory, ***docker-ctl*** provides functions to automatically build, run, stop and exec operations.
- Build NFS and SAMBA Docker Image base on CcentOS7
- Delete Docker Image
- Start Container (Auto config default service port mapping)
- Stop Container (stop and delete container)
- Execute commands in the Container


***docker-ctl*** command arguments:
```
build 
run [ nfs | smb | nfsmb ] [ <host-dir-path>:<container-dir-path>:<permission> ]
stop [ nfs | smb | nfsmb ]
exec <command and arguments>
status
```
Example1: build image
```
docker-ctl build
```
Example2: run docker with nfs service
```
docker-ctl run nfs /mnt/host_nfs_share:/mnt/docker_nfs_share
```
Example3: exec commands from docker
```
docker-ctl exec ip a
```

The Tool-kit will build a Docker Image with three commands below to provide basic NFS/SAMBA config and service start/stop.
- server-run   Start and Stop NFS/SAMBA Service
    - Arguments: [ status | restart | stop ] (Start services when no arugment specified)
    - Example1: docker-ctl exec server-run status
    - Example2: docker-ctl exec server-run restart
- config-nfs   Configure /etc/exports
    - Arguments: [ add | del ] <export-path> <export-options>
    - Exmaple1: docker-ctl exec config-nfs add /mnt (rw,async,norootsquash)
    - Example2: docker-ctl exec config-nfs del /mnt
- config-smb   Configure /etc/samba/smb.conf (Only provide anonymous access)
    - Arguments: [ add | del ] <share-name> <share-path>
    - Example1: docker-ctl exec config-smb add myshare1 /mnt
    - Example2: docker-ctl exec config-smb del myshare1

You could also access to the docker to configure and start service to fit your needs.
