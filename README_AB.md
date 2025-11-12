# Crie um network para os nós e o loadbalancer
    
    docker network create webnet
    
    docker network connect webnet loadbalacer
    docker network connect webnet node1
    docker network connect webnet node2
    docker network connect webnet node3

# Rode a imagem do AB

    docker run --rm --network webnet jordi/ab -n 500 -c 50 http://loadbalacer/

# Segunda forma de rodar sem usar docker

    apt-get update
    apt-get install apache2-utils 
    ab -n 500 -c 50 http://localhost:82/
 



