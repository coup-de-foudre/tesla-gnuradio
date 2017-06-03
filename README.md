# Tesla Signals

Simulating and creating signals for the Tesla coil.

> **Note** The code here is not functional. Currently the most interesting 
> bit may be the instructions below for how to get GNU Radio running in
> Docker with a UI.

## GNU Radio


### Mac installation

Using homebrew

https://github.com/andresv/homebrew-gnuradio


## Docker

## GNU radio docker

https://hub.docker.com/r/marcelmaatkamp/gnuradio/

### Mac setup

#### Graphical display

https://fredrikaverpil.github.io/2016/07/31/docker-for-mac-and-gui-applications/

You should be able to run:
```bash
ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 
xhost + $ip
docker run --rm --name firefox -e DISPLAY=$ip:0 -v /tmp/.X11-unix:/tmp/.X11-unix jess/firefox 
```

If you see a firefox screen pop up, you are winnning. Now try:

```bash
ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 
xhost + $ip
docker run -t -i --rm --entrypoint /bin/bash --name gnuradio \
  -e DISPLAY=$ip:0 -v /tmp/.X11-unix:/tmp/.X11-unix \
  -v ${PWD}/tutorial:/tutorial \
  -v ${PWD}/resources:/resources \
  --privileged marcelmaatkamp/gnuradio
```

To restart, try

```bash
ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}') 
xterm + $ip
docker start -ai gnuradio
```


#### Playing wav files

```bash
afplay path/to/file.wav
```

#### Converting mp3 to wav files

Install `ffmpeg`:

```bash
brew install ffmpeg --with-fdk-aac --with-ffplay --with-freetype \
  --with-libass --with-libquvi --with-libvorbis --with-libvpx \
  --with-opus --with-x265
```


Convert:
```bash
ffmpeg -i song.mp3 -acodec pcm_u8 -ar 22050 song.wav
```
