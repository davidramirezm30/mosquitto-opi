# mosquitto & mosquitto-clients <br>
![alt text](https://www.lolgast.nl/wp-content/uploads/2018/06/mosquitto-colour-deselected.png)
Porting official Eclipse mosquitto package to Docker image running on Orange Pi (ARMv7 32-bit or arm32v7) platform.

## Directories <br>
Create three directories for configuration, data and log.<br>
For doing so, copy and paste. <br><br>
```
sudo mkdir -p /docker/mosquitto/config
sudo mkdir -p /docker/mosquitto/log
sudo mkdir -p /docker/mosquitto/data
```
<br>

## Usage <br>
Copy and paste in the console of your Orange Pi or arm 32 bits device.<br><br>
```
sudo docker run -itd \
--name="mosquitto" \
--restart on-failure \
-p 1883:1883 \
-v /docker/mosquitto/config:/config \
-v /docker/mosquitto/data:/data \
-v /docker/mosquitto/log:/log \
davidramirezm30/mosquitto-opi
```
<br><br>
If you want to configure the user and the password change "USERNAME" for you own username.<br><br>
```sudo mosquitto_passwd -c /etc/mosquitto/pwfile USERNAME```<br><br>
i.e. If the `USERNAME` is orangepi, type `sudo mosquitto_passwd -c /etc/mosquitto/pwfile orangepi`

## Credits <br>
Build Dockerfile base on original from https://github.com/somsakc/docker-mosquitto git repository.
