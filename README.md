# docker

[Docker Commands](#docker-commands)  

## Let's start off with just building a docker image  

The bare essentials:  


`FROM alpine  
CMD [ "echo", "hello world" ]`

That is it. The FORM is the docker base image you are using ex. Alpine, Ubuntu:latest, or Ngnix.  
The container also needs something to do in this ex. we are echoing a string of text.  


`Next build it. 
docker build . `

^ we are using the period to indcate this is the directory to build this image in. 
### <a id="docker-commands"></a> Docker Commands
docker run -p 1234:80 nginx
docker run -p <server IP>:80 nginx

---

