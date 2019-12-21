# Hubot on Docker 
Let's Run Hubot on Docker Container. 

## HOW TO USE

### Create Env File

Create `./container/hubot/.env`

```terminal:terminal
$ touch ./container/hubot/.env
```

And edit it by `$ vim ./container/hubot/.env` to leave your hubot token.
(Use your favorite editor.)

```:.env
HUBOT_SLACK_TOKEN=<YOUR HUBOT TOKEN>
```

### Run Docker Container

```terminal:terminal
$ docker-compose up --build -d
```

## Notice

### HUBOT_SLACK_TOKEN

If you don't want to write your hubot token down on `.env` file, you can set the environment varible like this.

```terminal:terminal
$ export HUBOT_SLACK_TOKEN=<YOUR HUBOT TOKEN>
```

Edit `docker-compose.yml` as well. (remove `env_file` and add `environment`.)

```yaml:docker-compose.yml
version: '3'
services:
    hubot:
        build: ./container/hubot/
        volumes:
            - ./container/hubot/:/home/hubot/
        environment:
            - HUBOT_SLACK_TOKEN=${HUBOT_SLACK_TOKEN}
```

### `$ yo hubot comamnd` Constrain

I don't know why. But you can't call the envrionment variable in `Dockerfile`. 

```:Dockerfile
RUN yo hubot --owner=${HUBOT_OWNER} --name=${HUBOT_NAME} --description=${HUBOT_DESCRIPTION} --adapter "slack" 
# THIS WON'T WOKR FINE!!!
```

One more notice: `--owner` doesn't have to be an actual owner. It is fine to assign anything you like to the parameter.