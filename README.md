## Building

Commands

```sh
docker build -t username/project .
docker images

# run freshly build image and expose port 80
docker run -t -p 80:80 <IMAGE_ID>

# to look around inside the container use bash in interactive mode (-i)
docker run -t -i <IMAGE_ID> bash
```

## Quickly stop and remove all running containers and images

```sh
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -a -q)
```

## My docker images

- [zigomir/passenger-ruby211](https://index.docker.io/u/zigomir/passenger-ruby211/) - based on passenger/docker but with newest Ruby

## Issues I'm not really happy with yet

For now docker will upload whole context of project directory. Wait for `.dockerignore` feature discussed here on [github](https://github.com/dotcloud/docker/issues/2224).

## TODO

- [Auto start up](http://docs.docker.io/use/host_integration/)
- [Postgres](http://docs.docker.io/examples/postgresql_service/)
- [Linking containers together (Rails <3 PG)](http://docs.docker.io/use/working_with_links_names/)