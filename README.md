# Kitematic-docker

This Docker Image should give every Linux User the opportunity to use the Kitematic GUI.
(I've tried to install it on ubuntu and fedora, it both failed)

To start it, take a look at the firststart.sh script.

### Run the image

First, take the MIT-MAGIC-TOKEN from the host to be able to access your local Xorg-Server:


    mitcookies=$(xauth list)


Now the magic cookes are saved in the mitcookies variable.

Next, start your container:

    docker run --net host --name kitematic \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -e DISPLAY=$DISPLAY  \
    -e MAGICCOOKIES="$mitcookies" \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --privileged=true -t jonadev95/kitematic-docker


So, we need our X11 socket, the display variable, the magic cookies, and our docker socket. (And make it privileged to be able to write to the sockets)


If you want to start the container later again, just execute ```docker restart kitematic ``` (It will take a few seconds until it starts up)

That's all!
