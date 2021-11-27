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
- name: download vscode
  hosts: local
  tasks:
   - name: download vscode
     become: yes
     get_url:
       url: https://code.visualstudio.com/sha/download?build=stable&os=linux-rpm-x64
       dest: /tmp
   - name: Install package.
     yum:
       name: /tmp/code*.rpm
       state: present
       
