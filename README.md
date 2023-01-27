# **LEARNING:** Docker and Docker Compose

This was a small application developed to learn Docker and Docker Compose. 
It was based on [Nana Janashia's course on Docker](https://youtu.be/3c-iBn73dDE).

**Requirements:**
- Docker 
- Docker Compose

---

To test if Docker is installed, run the hello-world image from Dockerhub:

> `docker run hello-world`

Now we are ready to deploy our small Docker network: first, a docker image needs to be created from **our application**, be mindful of the last argument of the `docker build` command - it is the directory where the **Dockerfile** is located:
 
> `docker build -t my-app:1.0 .`

We can check we have the image created locally:

> `docker images`

This application and its containers can be deployed locally by using Docker Compose, as follows:

> `docker-compose -f Dockercompose.yaml up`

It will spin three containers in one Docker Network:
- One running **MongoDB**, bound to `localhost:27017` (from an image in Dockerhub)
- One running **mongo-express**, bound to `localhost:8080` (from an image in Dockerhub)
- One running **a simple NodeJS app**, bound to `localhost:3000` (from the image we built previously)

In the web app, one can change the fields of a form, and this data is saved in MongoDB. The container running MongoDB has a persistent local volume attached to the directory where MongoDB stores data ~ Inside the container, it is `/data/db`, and locally, the volume is stored in `/var/lib/docker/volumes/my-app_mongo-data` - this means once that container is stopped, data is persisted locally - if the container is started again, data will still be there.

We can check all three containers are up and running with:

> `docker ps`

And we can see the virtual network is also up and running with:

> `docker network ls`

Now try accessing `localhost:3000` and `localhost:8080` in any web browser and play around with the app + check if MongoDB is updated!

To bring the network and containers down, simply do: 

> `docker-compose -f Dockercompose.yaml down`

---
**TODO:**
- Add shell script to install Docker and Docker Compose.

