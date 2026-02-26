### 1. Собрать образ из Dockerfile.molecule

Находясь в корне проекта:

Код

```
docker build -t molecule-local -f Dockerfile.molecule .
```

После сборки:

Код

```
docker images | grep molecule-local
```

Ты увидишь:

Код

```
molecule-local   latest   <id>   <size>
```

Теперь команда:

Код

```
docker run --privileged -it --rm \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $(pwd):/opt/vector-role \
  -w /opt/vector-role \
  molecule-local bash
```



## Проверка

После запуска контейнера:

Код

```
molecule --version
```

и затем:

Код

```
molecule test
```


## Если хочешь, можно упростить запуск

Сделай alias:

Код

```
alias mol='docker run --privileged -it --rm \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $(pwd):/opt/vector-role \
  -w /opt/vector-role \
  molecule-local'
```

Теперь запуск:

Код

```
mol bash
```
