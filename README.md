# Docker-Container-Learning

### Add a dev container
- ```f1```, type ```add dev container``` and select ```Remote Containers: Add Development Container Configuration Files```
-  ```.devcontainer``` will be added to the project

- ```f1```, type ```reopen in container```, and select ```reopen in container```
you will find the container like below
![](https://github.com/chung-kai-eng/Docker-Container-Learning/blob/main/figure/screen%20shot.png | width=200)


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

### Flask
```shell=
// for local usage
$ export FLASK_APP=app
$ flask run

// for external visibility (make it publicly)
$ flask run --host=0.0.0.0
```
