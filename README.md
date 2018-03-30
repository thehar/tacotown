# tacotown
Deployable Jenkins through Rancher

## Requirements
* Docker for Mac
* Virtualbox

# MacOS and Rancher

Get Rancher up and running locally. Fire up a Terminal and here's some commands:

```
$ docker run -d --restart=unless-stopped -p 8080:8080 rancher/server:stable
$ docker logs <replace with rancher server run id>
$ open http://localhost:8080
$ sudo ipconfig getifaddr en0
$ docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso tacotown01
$ docker-machine create -d virtualbox --virtualbox-boot2docker-url https://releases.rancher.com/os/latest/rancheros.iso tacotown02
```

### Add tacotown hosts to Rancher

Lets change the IP of Rancher first. Navigate to `Admin` -> `Settings`.

Select something else and throw in http://yourip:8080.

Next lets hop over to `Infrastructure` -> `Hosts`. Add in your IP in the blank field, plus copy paste the Rancher agent URL.

```
sudo docker run --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v1.2.9 http://172.16.46.5:8080/v1/scripts/9D2BE0FF442EB1B3B533:1514678400000:aaBBcDE1fghiJKlM2nO3P4qR4s5
```

Next install Rancher agent on both tacotown machines.

```
$ docker-machine ssh tacotown01
$ docker-machine ssh tacotown02
```

Now we'll follow http://rancher.com/deploying-a-scalable-jenkins-cluster-with-docker-and-rancher/

# Credit
Immendes (https://gist.github.com/lmmendes/fbed32a452cf02d2a1095658795cb3d2)
