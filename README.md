Задача 1: https://hub.docker.com/layers/sirm1ssalot/custom-nginx/1.0.0/images/sha256-bc1ce85465c763c97b560a96ceb1e2b3c45e4bbbd8c6026beac697268b0332b8?context=repo

Задача 2: 
![image](https://github.com/nameless517/shdevops2/assets/60939929/fc425120-d0c0-4ad0-ad66-227035d3908b)

Задача 3:
.3 Контейнер остановился, т.к. терминал получил команду завершения процесса.
.10 Во время работы внутри контейнера мы сменили порт, в который идет трансляция nginx, а т.к. при запуске контейнера мы назначили маппинг 8080:80, ни докер ни хостовая система не знают о том, что nginx будет показывать что то на другом порту.
.11 Для актуализации конфигурации требуется поменять настройки контейнера на хосте, в файлах hostconfig.json и config.v2.json, в них нужно указать требуемый маппинг портов, предварительно остановив контейнер и службу docker. После внесения изменений нужно включить службу и контейнер.
![image](https://github.com/nameless517/shdevops2/assets/60939929/50e45490-064c-4924-b18b-68ab9a494edb)
![image](https://github.com/nameless517/shdevops2/assets/60939929/3db16790-801b-407a-904e-eabecbc85730)
![image](https://github.com/nameless517/shdevops2/assets/60939929/6c19c421-8fd9-49db-bd3c-166fb4f79ab4)

Задача 4:
![image](https://github.com/nameless517/shdevops2/assets/60939929/9b3afcb4-0bb4-4a84-be5b-7f6ff112d5e7)
![image](https://github.com/nameless517/shdevops2/assets/60939929/ac944e3a-e3bf-4743-a06b-d63c25ef631f)
![image](https://github.com/nameless517/shdevops2/assets/60939929/fe14d92e-610b-4846-a317-227568708566)


Задача 5:
![image](https://github.com/nameless517/shdevops2/assets/60939929/09db4c51-7318-4567-b408-5527f67b8958)
![image](https://github.com/nameless517/shdevops2/assets/60939929/4a8525af-e60a-44b2-bd70-d2a03610dfa1)
![image](https://github.com/nameless517/shdevops2/assets/60939929/9d70848d-52a1-425c-b116-2b942830cfdd)
![image](https://github.com/nameless517/shdevops2/assets/60939929/53bc1fa8-caeb-4e85-8726-30dcd0cfd711)




.6 После удаления файла docker-compose.yaml, docker compose находит контейнеры, принадлежащие другому проекту с тем же именем. 
