# podman-nvidia-cuda-ocl-sdk

## Tested on Fedora 32 x64 Live CD 

```bash
sudo tee /etc/yum.repos.d/nv-docker.repo <<EOF
[container]
name=container
baseurl=https://nvidia.github.io/libnvidia-container/centos7/\$basearch

[runtime]
name=runtime
baseurl=https://nvidia.github.io/nvidia-container-runtime/centos7/\$basearch
EOF


sudo dnf -y --nogpg install nvidia-container-toolkit podman mc make

F=/etc/nvidia-container-runtime/config.toml
sudo cp $F $F.bac
sudo tee $F <<EOF
disable-require = false
#swarm-resource = "DOCKER_RESOURCE_GPU"

[nvidia-container-cli]
#root = "/run/nvidia/driver"
#path = "/usr/bin/nvidia-container-cli"
environment = []
#debug = "/var/log/nvidia-container-toolkit.log"
#ldcache = "/etc/ld.so.cache"
load-kmods = true
no-cgroups = true
#user = "root:video"
ldconfig = "@/sbin/ldconfig"
#alpha-merge-visible-devices-envvars = false

[nvidia-container-runtime]
debug = "/var/log/nvidia-container-runtime.log"
EOF

```
