# VS_code_prax

This our project root folder. ReadMe.md file is typically the first file to create and should contain a brief description of the project and high-level overview.

Installing Apache/Superset from dockerhub: https://hub.docker.com/r/apache/superset
```bash
docker run -d -p 8081:8088 -e "SUPERSET_SECRET_KEY=4ty08247gt2b743yg22r3g245uy" --name superset_tmp apache/superset:master-py310-arm

docker exec -it superset_tmp superset fab create-admin --username adler --firstname Priit --lastname Adler --email adler@ut.ee --password minu_parool_1

docker exec -it superset_tmp superset db upgrade

docker exec -it superset_tmp superset init

# not running examples for now...
docker exec -it superset_tmp superset load_examples
```

Edit [Dockerfile](Dockerfile) to include the additional packages we need and then run:
```bash
docker build -t my/superset:duckdb .
```

After that we first need to stop and remove the old container and then run the new one:
```bash
docker run -d -p 8081:8088 -v ${PWD}:/data:rw -e "SUPERSET_SECRET_KEY=4ty08247gt2b743yg22r3g245uy" --name superset_tmp my/superset:duckdb
# also rerun the admin creation, db upgrade and init commands
```
