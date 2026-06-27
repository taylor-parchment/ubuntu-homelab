
Since this was set up using existing hardware and OSes, my server's laptop is Ubuntu Desktop. Ideally, this would be an Ubuntu Server installation, but for my use-case, I have not encountered major issues yet.

## Prepping Server Laptop

The first steps I took were directly on the Surface laptop. I updated Ubuntu, installed SSH, and set the device hostname.
```
sudo apt update
sudo hostnamectl set-hostname homelab-server
sudo apt install openssh-server
```
Then SSH needs to be enabled and started.
```
sudo systemctl enable ssh
sudo systemctl start ssh
```
I just need the server device's IP before I can access it via SSH.
```
ip addr
```
From here, I did all configuring on my main Windows laptop via SSH. From Powershell:
```
ssh <username>@<server-ip>
```

![ssh from Windows](screenshots/SSH-from-windows.PNG)

## Samba

There are Windows, Linux, and Mac devices in our house, so quick filesharing across OSes over the network is the first thing I wanted to set up. 

To install Samba:
```
sudo apt install samba
```
Set up the shared folder with a test file:
```
mkdir ~/shared
echo "test" > ~/shared/test.txt
```
The shared folder needs to specified in the Samba config file at `/etc/samba/smb.conf`.

For the moment, since I'm the only one accessing the folder, I set myself as the only user.

![[samba-config.png]]

Lastly, a password should be set:
```
sudo smbpasswd -a <username>
sudo systemctl restart smbd
```
After entering the credentials in Windows, I had access to the folder! Now moving things between the server is super easy and can be done in Windows' default file explorer.

![[windows-file-access.png]]

## Netdata

To see an overview of the system in a dashboard, I installed Netdata. For my case, it's more information than I know what to do with, but it's good to be able to remotely monitor all the important system details like CPU load, RAM usage, storage and networking stats.

Using the recommended installation method on the site (with telemetry disabled):
```
wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh --disable-telemetry
```
After that, everything can be monitored on a browser at port 19999 by default.

![[netdata.png]]

## Docker

There are several services I would like to set up that can be deployed with Docker.

I got started using the [Docker installation guide for Ubuntu Linux](https://docs.docker.com/engine/install/ubuntu/#install-from-a-package). First, set up Docker's apt repository:
```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```
Then install Docker packages:
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Then, it just needs to be started, and a test image can be run:

```
sudo systemctl start docker
sudo docker run hello-world
```
Now, with just a `yaml` file and a single command, I can deploy any service that works with Docker.

One thing I had to do before I could run anything was set permissions for my user with the following:
```
sudo usermod -aG docker <username>
```

## Jellyfin

Jellyfin's Docker `yaml` example can be found on their [site](https://jellyfin.org/docs/general/installation/container). I removed a lot of the optional settings. 

The important setting is the media source, which I linked to a file in my shared Samba drive. That way, I can simply drag and drop a file from Windows into my shared folder and access it anywhere in Jellyfin.

The `yaml` file goes in a folder called `jellyfin`, and in that folder, I just need to run:

`docker compose up`

After setting a username and password in the Jellyfin application, it's good to go!

The home screen looks like this after adding a few movies and shows.

![[Pasted image 20260627183009.png]]
## Lute

The exact same process can be done to install the language learning tool Lute with Docker. I followed the Docker setup guide on the [site](https://luteorg.github.io/lute-manual/install/install.html#using-docker).

After importing a few of my previous articles, the home screen looks like this:

![[lute-home.png]]
