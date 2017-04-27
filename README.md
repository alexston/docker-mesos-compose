#### Run Mesos and Marathon in Docker with Docker Compose!

Run:

```
docker-compose up -d
```

To stream log output, simply run:

```
docker-compose logs
```

Great! Now let's pop open the Mesos, Marathon, & Chronos' UI like so:

```
open http://localhost:5050/ # open Mesos UI
open http://localhost:8080/ # open Marathon UI
open http://localhost:4400/ # Open Chronos UI
```

Let's launch a simple app through [Marathon's REST API](https://mesosphere.github.io/marathon/docs/rest-api.html) like so:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localhost:8080/v2/apps -d '
{
    "id": "hello",
    "cpus": 0.1,
    "mem": 32,
    "cmd": "echo hello; sleep 10"
}'
```

And now for a Docker container:

```
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  localhost:8080/v2/apps -d '
{
    "id": "inky",
    "container": {
        "docker": {
            "image": "mesosphere/inky"
        },
        "type": "DOCKER",
        "volumes": []
    },
    "args": ["hello"],
    "cpus": 0.2,
    "mem": 32.0,
    "instances": 1
}'
```



