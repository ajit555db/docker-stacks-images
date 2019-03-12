https://docs.docker.com/get-started/
https://docs.docker.com/compose/compose-file/
https://cloud.docker.com/repository/list

# Startup

    export AJIT_SERVER_DIR="/home/ajit/OneDrive/Codebook/k8s/"
    export AJIT_SERVER_IP="192.168.0.116"
    sshpass -p 'ajit@123' ssh -t ajit@$AJIT_SERVER_IP "cd ${AJIT_SERVER_DIR} ; bash; "
    cd ~/OneDrive/Codebook/k8s/container-images/app-samples/stack-demo-py-redis-counter/

# Part 1 - Orientation
https://docs.docker.com/get-started/

## Terms

Image 

    An image is an executable package that includes everything needed to run an application--the code, a runtime, libraries, environment variables, and configuration files.

Container 

    A container is a runtime instance of an image--what the image becomes in memory when executed (that is, an image with state, or a user process). A container runs natively on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

Service

    Services are really just “containers in production.” A service only runs one image, but it codifies the way that image runs—what ports it should use, how many replicas of the container should run so the service has the capacity it needs, and so on. Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.

    Services are defined, run, and scaled on the Docker platform using "docker-compose.yml" file.

    In a distributed application, different pieces of the app are called "services". For example, if you imagine a video sharing site, it probably includes a service for storing application data in a database, a service for video transcoding in the background after a user uploads something, a service for the front-end, and so on.

Stack

    A stack is a group of interrelated services that share dependencies, and can be orchestrated and scaled together. A single stack is capable of defining and coordinating the functionality of an entire application (though very complex applications may want to use multiple stacks).

Stack can not build images unlike docker-compose, so build the image first.

# Build image

docker build --tag=demo-py-redis-counter .


# Stacks
https://docs.docker.com/get-started/part5/

    docker swarm init
    docker stack deploy -c docker-compose.yml stack-demo-py-redis-counter

    docker service ls
    docker container ls -q 
    docker service ps <service>

http://192.168.0.116
http://192.168.0.116:8080/

## Take down the app and the swarm

    docker stack rm stack-demo-py-redis-counter
    docker swarm leave --force