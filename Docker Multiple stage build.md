

Dockerfile 每個額外指令，都會新增 **圖層 (layer)**: Lots of unnecessary artifacts should be cleaned up before moving to the next layer

Docker added a new feature that allowed the creation of multi-stage builds.
- helps with optimizing the files
- improves their readability
-  easire to maintain




$ docker build --target publish -t gregsimages/popkorn:latest .



### [Docker file](https://docs.docker.com/get-started/02_our_app/)
- a text-based script of instructions that is used to create a container image

- check that the file ```Dockerfile``` has no file extension like ```.txt```, or it will result in an error in the next step




### Multi container apps
- Each container should do one thing and do it well
    - Separate containers let you version and update version in isolation
    - When using a container for the database locally, you won't want to ship your database engine with your app
    - Running multiple processes will require a process manager, increasing cmoplexity to container startup/ shutdown
- **Networking**: let one container to talk to another
    - Two ways to put a container on a network
        1. Assign it at start
        2. connect an existing container
1. Create the network
```docker=

```