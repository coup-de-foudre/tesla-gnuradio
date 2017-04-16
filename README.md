# Tesla Signals

Simulating and creating signals for the Tesla coil.


## GNU Radio


### Mac installation

Using homebrew

https://github.com/andresv/homebrew-gnuradio


## Docker

## GNU radio docker

https://hub.docker.com/r/marcelmaatkamp/gnuradio/

### Mac setup

#### Audio

```
brew install pulseaudio
brew install paprefs
```

Install on the `gnuradio` docker container:

```
sudo apt-get install -y pulseaudio
```

#### Graphical display

https://fredrikaverpil.github.io/2016/07/31/docker-for-mac-and-gui-applications/

You should be able to run:
```
ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 
xterm + ip
docker run --rm --name firefox -e DISPLAY=$ip:0 -v /tmp/.X11-unix:/tmp/.X11-unix jess/firefox 
```

If you see a firefox screen pop up, you are winnning. Now try:

```bash
docker run -t -i --entrypoint /bin/bash --name gnuradio -e DISPLAY=$ip:0 -v /tmp/.X11-unix:/tmp/.X11-unix --privileged marcelmaatkamp/gnuradio 
```

To restart, try

```bash
ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 
xterm + ip
docker start -ai gnuradio
```
