# Learn MongoDB

Docker Compose file that will provide a MongoDB instance along with a web-based database tool incase you don't already have a db tool. Monitoring is also included to show how that would work as well.

## Why did I make another "basic" tutorial?
A lot of times I found myself having to leverage multiple tutorials in order to holestically create what I feel was a full working demo.  I do my best to credit sources I leveraged to create this and I hope you find as useful as I did.  I've built these specifically to help folks I lead to be able to learn not just the tool, but also how to easily add monitoring which I find helps during development and testing.

## Docker vs Podman
I have tested this using [Docker](https://docker.com) and [Podman](https://podman.io/).  I personally use Podman and can confirm the `docker compose` commands will work seemlessly.

## How to connect to MongoDB from Mongo Express (via Container)
1. Run this command: ``` docker compose up -d mongodb mongo-express ```
2. Open browser to ``` localhost:8081 ```

## How to turn on/use Monitoring Services 

1. Spin up all services docker command: ``` docker compose up -d --no-recreate ```
    - I included ``` --no-recreate ``` incase you already had MongoDB and Mongo Express running it wouldn't restart them.
2. You can verify ```mongodb-exporter ``` is running by running this command in terminal or powershell: ``` curl http://localhost:9216/metrics ```
    - You should see an output like below, but don't worry about the counts so long as they already all 0
    ```
    collector_scrape_time_ms{collector="collstats",exporter="mongodb"} 2
    collector_scrape_time_ms{collector="dbstats",exporter="mongodb"} 3
    collector_scrape_time_ms{collector="diagnostic_data",exporter="mongodb"} 42
    collector_scrape_time_ms{collector="general",exporter="mongodb"} 0
    collector_scrape_time_ms{collector="indexstats",exporter="mongodb"} 1
    collector_scrape_time_ms{collector="replset_status",exporter="mongodb"} 0
    collector_scrape_time_ms{collector="top",exporter="mongodb"} 2
    ```
3. You can verify Prometheus is running by going to this page: http://localhost:9090/targets?search=
    - You should see both targets UP and in green status
4. Open Grafana by going to ``` http://localhost:3000 ```
    - Login with 
        - user: admin
        - password: admin
        - you will be prompted to change the password, but for testing purposes you can just "change it" to admin (LOL)
    - You will want to add a Data Source 
        - Choose Prometheus
        - update url to ``` http://prometheus:9090 ```
        - Click `Sve & test` button
    - Go to `Dasboards` and choose `+import`
        - Where it says `Import via grafana.com` type ``` 12079 ``` and click `Load`
            - You will need to set the `Data Source` to Prometheus data source you just created
    - You should see a populated grafana dashboard!
    - Sometimes you will need to tweak the time period at the beginning for values to populate.  I usually try "Last 30 minutes"
## Sources
- MongoDB on [DockerHub](https://hub.docker.com/_/mongo)
- [MongoDB Exporter](https://github.com/percona/mongodb_exporter/) 
- [MongoDB Exporter commands](https://forums.percona.com/t/prometheus-mongodb-exporter/16447)

