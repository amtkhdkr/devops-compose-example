# devops-compose-example
A sample application showing how to use Nginx, Go and Percona SQL.
The backend consists of a simple Go application which connects to the DB and uses Nginx as a proxy load balancer.

Project structure:
```shell
.
├── backend
│   ├── Dockerfile
│   ├── go.mod
│   └── main.go
├── db
│   └── password.txt
├── compose.yaml
├── proxy
│   ├── conf
│   └── Dockerfile
└── README.md
```

The compose file defines an application with three services proxy, backend and db. When deploying the application, docker compose maps port 80 of the proxy service container to port 80 of the host as specified in the file. To deploy multiple replicas of the backend, simply use the correct flag during the [up command](https://docs.docker.com/compose/reference/up/) option --scale backend=NUM

# Deploy with Docker Compose
```shell
$ docker compose up -d --scale backend=2
```
After the application starts, navigate to `http://localhost:80` in your web browser or run:
```
$ curl localhost:80
["Blog post #0","Blog post #1","Blog post #2","Blog post #3","Blog post #4"]
```

Stop and remove the containers
```
$ docker compose down
```
