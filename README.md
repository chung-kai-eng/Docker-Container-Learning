# Docker-Container-Learning

- [**Dockerfile cheatsheet**](https://devhints.io/dockerfile)
- [**Docker-compose cheatsheet**](https://devhints.io/docker-compose)
- relationship between remote container and vscode
![](https://github.com/chung-kai-eng/Docker-Container-Learning/blob/main/figure/Local%20and%20Container%20relationship.png)

### Add a dev container
- ```f1```, type ```add dev container``` and select ```Remote Containers: Add Development Container Configuration Files```
-  ```.devcontainer & Dockerfile``` will be added to the project (This two files came from the VSCode dev containers)

- ```f1```, type ```reopen in container```, and select ```reopen in container```
you will find the container like below
![](https://github.com/chung-kai-eng/Docker-Container-Learning/blob/main/figure/screen%20shot.png)


- ```Ctrl``` + ``` ` ```: open the terminal

```shell=
$ python --version
$ pip3 install --user -r requirements.txt // can put in ```postCreateCommand```
```

### ```.devcontainer```
- ```build```: define how th container will be created
- ```settings```: copy machine-specific settings into the container. By adding them to the ```settings```,  you ensure that anyone who opens this project gets these specific VS Code settings.  
- the rest of the section refers to dealing directly with project configuration
    - ```extensions```: specify which **VSCode extensions** should be installed in VSCode when it connects to the container
    - ```postCreateCommand```: let you run any commands that you want after the container is created. Can automatically do default, since other might not know the default action

### Install VSCode extension example
- ```f1```, select extension and search the extension you want e.g. ```jinja``` > install it > Right click the extension to **Copy extension ID** > add the ```extension ID``` 
```json=
// Add the IDs of extensions you want installed when the container is created.
"extensions": [
    "ms-python.python",
    "ms-python.vscode-pylance"
],
```

### ```Dockerfile```
- If you want to add software beyond what's available in those images or preconfigured dev containers? (beyond devcontainer.json  docker image), you have to install different software every time you rebuild your container. The most efficient practive is to install software through your Dockerfile.
    - You might want to include ```Node.js, SQL...``` in any of your dev containers, so install software by write the command in Dockerfile
        - e.g. ```apt-get```, ```apt``` for Ubuntu
- The ```RUN``` command creates a new layer. Layers are how the container knows what has changed and what in the container needs to be updated when you rebuild it. You should try to keep related logic together in the same RUN command so that you don't create unnecessary layers.
- The ```\``` denotes a line break at the end of a line. You need it for multiple-line commands.
The ```&&``` is how you add a command to the ```RUN``` line.
The ```DEBIAN_FRONTEND``` export avoids warnings when you go on to work with your container. When you're adding other software, you might instead use other flags or parameters, such as ```-y```.
The ```-y``` ensures that ```apt-get``` doesn't prompt you to confirm that you want to finish the installation. These prompts would cause the container build to fail because nobody would be there to select ```Y``` or ```N```.

```yml=
RUN apt-get update \
&& apt-get install -y curl ca-certificates \
&& curl -sL https://deb.nodesource.com/setup_14.x | bash \
&& apt-get install nodejs \
&& node -v \
&& npm -v \
```

### Flask
```shell=
// for local usage
$ export FLASK_APP=app
$ flask run

// for external visibility (make it publicly)
$ flask run --host=0.0.0.0
```
