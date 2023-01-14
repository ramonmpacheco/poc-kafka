# POC-KAFKA
## POC COM KAFKA
<br/>

> PARA VER O NOME DO SERVIÇO/CONTAINER
> 
> ```docker-compose ps```

> PARA VER OS LOGS NO DOCKER
> 
> ```docker logs poc-kafka-kafka-1```

> PARA ACESSAR O CONTAINER
> 
> ```docker exec -it poc-kafka-kafka-1 /bin/bash```

> COMANDOS MAIS USADOS
> 
> - kafka-topics
> - kafka-console-producer
> - kafka-console-producer

> PARA CRIAR UM TOPICO VIA LINHA DE COMANDO
> 
> ```kafka-topics --create --topic=teste --bootstrap-server=localhost:9092 --partitions=3```
> 
> - --topic <String: topic>                  The topic to create, alter, describe
                                           or delete. It also accepts a regular
                                           expression, except for --create
                                           option. Put topic name in double
                                           quotes and use the '\' prefix to
                                           escape regular expression symbols; e.
                                           g. "test\.topic".
>
> - --bootstrap-server <String: server to    REQUIRED: The Kafka server to connect
  connect to>                              to. In case of providing this, a
                                           direct Zookeeper connection won't be
                                           required.
>
> - --create                                 Create a new topic.
>
> - --partitions <Integer: # of partitions>  The number of partitions for the topic
                                           being created or altered (WARNING:
                                           If partitions are increased for a
                                           topic that has a key, the partition
                                           logic or ordering of the messages
                                           will be affected). If not supplied
                                           for create, defaults to the cluster
                                           default.
>
> #output
> 
> Created topic teste.


> PARA LISTAR OS TOPICOS:
> 
> ```kafka-topics --list --bootstrap-server=localhost:9092```
>
> #output
> __consumer_offsets
>
> teste
>
> - ignore os topicos do _confluent-controlcenter
>
> - __consumer_offsets: guarda qual offset determinado consumer está no momento da leitura dos topicos