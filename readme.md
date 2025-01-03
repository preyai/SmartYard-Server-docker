# SYS - SmartYard-Server
#### Only test, not for production!
1. ### Clone repos 
    ```
    make sys_clone_libs
    ```
2. Create docker shared network
```shell
docker network create --driver bridge --subnet=192.168.100.0/24 shared-network-dev 
```

3. ### Edit config files
    #### set your external ip or domain in example config files:
    - client config: docker/example_conf/rbt_client_config.json
    - server config: docker/example_conf/rbt_server_config.json

    ```
    sed -i 's/127.0.0.2/rbt-domain.com/g' docker/example_conf/SmartYard-Server_*.json
    ```

4. ### Make your SSL certificate
    Make ssl for NGINX and copy to dir docker/nginx/certs:  
    use [acme.sh](https://github.com/acmesh-official/acme.sh)
    copy do this dir or use default or use self-signed SSL:
   ````
   docker/nginx/conf.d/certs/nginx.key
   docker/nginx/conf.d/certs/nginx.crt
   ````

5. #### Copy configs to SmartYard-Server project
    copy server, client and asterisk configs
    ```
    make sys_copy_configs
    ```

6. ### Start SmartYard-Server
    ```
    sudo make sys_start
    ```

7. ### Init db, set admin password
    ````
    docker exec -it rbt_app php server/cli.php --init-db
    docker exec -it rbt_app php server/cli.php --init-clickhouse-db
    docker exec -it rbt_app php server/cli.php --admin-password=<your very secret admin password>
    docker exec -it rbt_app php server/cli.php --reindex
    docker exec -it rbt_app php server/cli.php --install-crontabs
    ````

8. ### Stop SmartYard-Server
    ```
    sudo make sys_down
    ```
   
---
Create shared network
```shell
docker network create --driver bridge --subnet=192.168.100.0/24 shared-network-dev 
