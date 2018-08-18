# BTX-VNC-docker-qtWallet
Start a Bitcore (BTX) qt-Wallet in a docker container and connect with VNC

## Build
```sh
git clone https://github.com/BTX-VNC-docker-qtWallet
cd BTX-VNC-docker-qtWallet
docker build -t btx-vnc-docker-wallet .
```

## Getting Started
```sh
mkdir /home/<username>/.bitcore
docker run -it --name btx-docker-wallet --rm -p 5900:5900 -v=/home/MyUser/.bitcore:/root/.bitcore btx-docker-wallet
```
Note: Change <username> to your user.

The prior step creates and runs a container and gives you a command prompt on it.  From that prompt:

```sh
. /entrypoint.sh
bitcore-qt &
x11vnc -display :1 -usepw
```
entrypoint.sh sets a machine id and then sets up Xvfp so that bitcore-qt can use it.
Next, execute bitcore-qt in demonic mode (see the trailing &)
Finally, execute x11vnc so that we can see bitcore-qt from a VNC viewer on the host. When this first runs, it will ask for a password.  You'll need this password in your VNC viewer.

Next, 
```
docker ps
```
This will give you a display of all your running containers. Hopefully you'll see **btx-docker-wallet** and can determine which port on the local host it's using.


## VNC Connection
Finally, run your VNC viewer of choice and connect to that port on localhost. For example, if you see that port 5900 in the container has been mapped to port 32768 on the host, you would connect to 127.0.0.1:32768. Recall that you'll need the password you set for x11vnc earlier.
