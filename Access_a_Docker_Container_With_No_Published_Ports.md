#### Question
    In this challenge, you'll need to interact with a Docker container called networking-is-fun. This container has an Nginx server listening on 0.0.0.0:80. Your task is to send an HTTP request to this server. The catch is that the container doesn't have any ports published, and there is no HTTP client installed inside the container. The playground will also try its best to prevent execution (i.e., docker exec) of any commands in the container, so you won't be able to install anything extra into it either. But this shouldn't stop a real container ninja from accessing the Nginx, right?

#### Solution
1. Checking Running container
    ```
    docker ps

    1d87e21eb617   nginx:alpine-slim   "/docker-entrypoint.…"   9 minutes ago   Up 9 minutes   80/tcp    networking-is-fun
    ```
2. Spawn a new container on same network where other container is running. 
    ```
    docker run -d --rm --network container:networking-is-fun --name temp-nets alpine:latest sleep infinity
    ```
3. Now exec into that conatiner 
    ```
    docker exec temp-nets wget -qO http://localhost:80
    ```
