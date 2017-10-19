build:
	docker build -t pgbench .

createtestdata:
	docker exec -e SCALE=50 -it pgbench1 /createtables.sh

runtest:
	docker exec -e THREAD=8 -e CONNECTION=32 -e SCALE=50 -it pgbench1 /run.sh

clean:
	docker rm -f pgbench1

shell:
	docker exec -it pgbench1 bash

clearalldata:
	sudo rm -rf $(HOME)/tmppgbenchdata/*

startdb:
	docker run --name pgbench1 \
	-e POSTGRES_PASSWORD=docker \
	-e POSTGRES_USER=postgres  \
      -p 5432:5432 \
      -v $(HOME)/tmppgbenchdata/:/data \
       -d pgbench

stopdb:
	docker stop pgbench1

initdb:
	docker run --name pgbench1 \
     	-e POSTGRES_PASSWORD=docker \
     	-e POSTGRES_USER=postgres \
         --publish 5433:5432 \
         --volume $(HOME)/tmppgbenchdata:/data \
         --rm pgbench /initdb.sh ;\
         	docker run --name pgbench1 \
         	-e POSTGRES_PASSWORD=docker \
         	-e POSTGRES_USER=postgres  \
               -p 5432:5432 \
               -v $(HOME)/tmppgbenchdata/:/data \
                -d pgbench

searchtags:
	 wget -q https://registry.hub.docker.com/v1/repositories/postgres/tags -O -  | sed -e 's/[][]//g' -e 's/"//g' -e 's/ //g' | tr '}' '\n'  | awk -F: '{print $3}'

pgbench__:
	create dataase test1;
	pgbench -U postgres -h localhost -i -s 50 test1
	pgbench -U postgres -h localhost -c 10 -j 2 -t 10000 test1
