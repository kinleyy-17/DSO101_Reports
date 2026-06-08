* Jenkins is a tool that automatically builds, test and delivers the code.
* so you don't have to do it manually every time when code base changes.
* Jenkins never do the deployment.
* deployment is done by scripts.
* IP address can change.
* MAC Address cannot change (Media Access Control)
* port number 8080
* **Port Mapping -** matching the port number with the IP address
* cannot add port mapping while the server is running



# PORT MAPPING

&#x09;-left side indicates external

&#x09;-right side indicates internal



**steps to open externally**
1.open a browser

2.enter "localhost:portnumber"

85974c22fe314dadb07bb07af26611c5 - password

pip is a package manager for python
a tool that installs and manages extra python code(libraries)
its like a pythons app store

**Task of pip**
install python libraries and packages
PIP -> Pip install packages
Pip is a tool named as pip inside the package

**Flask install**
*Python3 -m pip install flask*
**-m** means it is giving a instruction dont run a file instead find this module(pip) inside python and run it like a program

**task**
using for loop print triangle and reverse
using while loop print triangle and reverse
swaping(a,b =b,a)



# Docker Images
-behaviour of image is determined by webserver

# Steps on building a Docker Image
1.Create  file locallly - to work in a home directory (mkdir -p ~/myapp)
mkdir - creates a directory
-p - flag/option (parent)
~(tilde) -
flag is an extra instruction to add to a command to change how that command behaves, special setting that modifies the action 
example : mkdir -p myfolder

2.get inside the directory
cd ~/myapp

3. python app.py


Create app ----> write dockerfile ---> Build Image ---> Run

4.notepad dockerfile 

5.docker build -t flaskapp .

6.docker run -p 8080:8080 flaskapp

  Id CommandLine
  -- -----------
   1 mkdir -p ~/myapp
   2 cd ~/myapp
   3 python app.py
   4 pip install flask
   5 python app.py

# how to give a name tag
local image ---> Tag with username ---> push ---> Verify

**steps**
1. confirm your image exist
docker images

2. rebuild the image with username
docker build . -t username/imagename
docker build . -t kyserl11/flaskapp:latest

-t -> nametag

3. docker push username/imagename


# structure of dockerfile

1. FROM <base-image>
BASE-IMAGE - starting point of our docker image also known as foundation layer/starting layer\prebuilt image
eg: python:3.10 - pyhton app, node:18 - node.js app, engineX - web server, Ubuntu - general linux, alpine - light weight linux.

2. WORKDIR <app-dir>

3. COPY <files>
eg: COPY.py . current file

4. RUN <install-dependencies>


5. EXPOSE <port>
eg: creating open door/port

6. CMD ["RUN","app"]

*** virtualization vs Containerization ***
- Storage or memory usage
- seperate environment
- in containerization slim or light weight or very samll is always prefered