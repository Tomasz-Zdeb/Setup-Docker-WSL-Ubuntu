# Setup Docker on WSL with Ubuntu

Step by step guide to get **Docker** on **WSL** with **Ubuntu** distro.

## Docker engine installation

Install Ubuntu, and execute:

```bash
sudo apt-get update
```

```bash
sudo apt-get upgrade
```

```bash
sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2
```

```bash
curl -fsSL https://download.docker.com/linux/${ID}/gpg | sudo tee /etc/apt/trusted.gpg.d/docker.asc
```

```bash
echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

```bash
sudo apt update
```

```bash
sudo apt install docker-ce docker-ce-cli containerd.io
```

## Almost rootless access

It's actually kind of workaround. Under the hood `sudo` commands are executed withoud password needed.

```bash
sudo usermod -aG docker $USER
```

```bash
sudo visudo
```

sudoers file will be opened. Add:

* `%docker ALL=(ALL)  NOPASSWD: /usr/bin/dockerd`
* `%docker ALL=(ALL)  NOPASSWD: /usr/bin/docker`

Open or create `.bash_alliases` file in Your home directory and add:

* `alias docker='sudo docker'`
* `alias dockerd='sudo dockerd'`

## References

* [Dev article](https://dev.to/bowmanjd/install-docker-on-windows-wsl-without-docker-desktop-34m9)