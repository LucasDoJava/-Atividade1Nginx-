# Instalação dos serviços

    docker run -itd --name loadbalancer -p 82:80 nginx:1.29.3-alpine
    docker run -itd --name node1-v caminho/do/projeto:usr/share/nginx/html nginx:1.29.3-alpine
    docker run -itd --name node2 -v caminho/do/arquivo:usr/share/nginx/html nginx:1.29.3-alpine
    docker run -itd --name node3 -v caminho/do/arquivo:usr/share/nginx/html nginx:1.29.3-alpine

# Acesse o bash do loadbalancer

    docker exec -it loadbalancer sh

# Acesse o arquivo default.conf

    cd etc/nginx/conf.d
    nano default.conf

# Edite o arquivo da seguinte forma

    upstream webfront {
        server node1:ip;
        server node2:ip;
        server node3:ip;
    }

    server {
        listen 80;

        location / {
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://webfront;
        }
    }

# Reinicie todos os container 

    docker restart loadbalancer node1 node2 node3
