build:
	docker build -t kutuni/postgresql:10-alpine .

shell:
	docker exec -it postgres bash

run:
	docker run --name postgres \
	-e POSTGRES_PASSWORD=docker \
	-e POSTGRES_USER=postgres -it \
      --publish 5432:5432 \
      --volume $(HOME)/tmppgdata:/data \
       -d kutuni/postgresql:10-alpine


clean:
	docker rm -f postgres
