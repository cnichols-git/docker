##Cnichols
#
# 
FROM ubuntu:latest
RUN apt-get update && apt-get install firefox -y && groupadd -g 1000 chris && useradd -d /home/chris -s /bin/bash/ -m chris -u 1000 -g 1000
RUN chown -R chris /home/chris
USER chris
ENV HOME /home/chris
CMD getent passwd chris
CMD /usr/bin/firefox


# To launch this run this:
# sudo docker run -e DISPLAY -v $HOME/.Xauthority:/home/chris/.Xauthority --net=host <build_name>