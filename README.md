# Learn MongoDB

Docker Compose file that will provide a MongoDB instance along with a web-based database tool incase you don't already have a db tool. Monitoring is also included to show how that would work as well.

## Why did I make another "basic" tutorial?
A lot of times I found myself having to leverage multiple tutorials in order to holestically create what I feel was a full working demo.  I do my best to credit sources I leveraged to create this and I hope you find as useful as I did.  I've built these specifically to help folks I lead to be able to learn not just the tool, but also how to easily add monitoring which I find helps during development and testing.

## Docker vs Podman
I have tested this using [Docker](https://docker.com) and [Podman](https://podman.io/).  I personally use Podman and can confirm the `docker compose` commands will work seemlessly.

## How to connect to MongoDB from Mongo Express (via Container)
1. Run this command: ``` docker compose up -d mongodb mongo-express ```
2. Open browser to ``` localhost:8081 ```

## Sources
MongoDB on [DockerHub](https://hub.docker.com/_/mongo)
[MongoDB Exporter](https://github.com/percona/mongodb_exporter/) 
[MongoDB Exporter commands](https://forums.percona.com/t/prometheus-mongodb-exporter/16447)

