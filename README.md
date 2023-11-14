Virt Manager on macOS
=====================

### Requirements

- Docker Desktop for Mac
- XQuartz

### Installation

1. Install XQuartz via Homebrew or download from https://www.xquartz.org/
```bash
brew install --cask xquartz
```

2. Install Docker Desktop for Mac via Homebrew or download from https://www.docker.com/products/docker-desktop
```bash
brew install --cask docker
```

### Preparation

1. Open XQuartz, go to settings, then Security and allow connections from Network-Clients.

![XQuartz Settings Screenshot](docs/settings.png)

2. Allow localhost connection to X11
```bash
xhost +localhost
```

### Running

Start Container with following commands.

```bash
docker volume create virt-manager-config
docker run -t -i --rm \
  -v virt-manager-cfg:/home/default/.config/:rw \
  --mount type=bind,src=/run/host-services/ssh-auth.sock,target=/run/host-services/ssh-auth.sock \
  --name virt-manager \
   tyrola/virt-manager:latest
```
