# Some log records are missing after restarting fluentd

```
docker -v
Docker version 18.06.1-ce, build e68fc7a

docker-compose -v
docker-compose version 1.22.0, build f46880f

MacOS 10.14.0 (Mojave)
```

# Reproducing

- Clone this repo
- Check your docker and docker-compose versions
- Open "A" terminal, start app: ```docker-compose up -d --build```
- Open "B" terminal, watch log: ```docker-compose logs -f```
- Stop fluent on "A": ```docker stop fluent```
- Check your logs on "B": fluent gracefully stoped
- Wait 6 seconds
- Start fluent on "A": ```docker start fluent```
- Check your logs on "B": check "msg": _number,_ **the numbering is not continuous.**

It is reproducible without docker-compose (docker run).
