##Cnichols
#
# 
FROM ubuntu:latest
RUN apt-get update && apt-get install -y firefox x11vnc xvfb
RUN echo "exec firefox" > ~/.xinitrc && chmod +x ~/.xinitrc
CMD ["v11vnc", "-create", "-forever"]
