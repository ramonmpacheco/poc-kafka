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
> 
> __consumer_offsets
>
> teste
>
> - ignore os topicos do _confluent-controlcenter
>
> - __consumer_offsets: guarda qual offset determinado consumer está no momento da leitura dos topicos

> PARA DESCREVER UM TÓPICO:
> 
> ```kafka-topics --bootstrap-server=localhost:9092 --topic=teste --describe```
> ~~~shell
> $ kafka-topics --bootstrap-server=localhost:9092 --topic=teste --describe
> #output
> Topic: teste    PartitionCount: 3       ReplicationFactor: 1    Configs:
>         Topic: teste    Partition: 0    Leader: 1       Replicas: 1     Isr: 1
>         Topic: teste    Partition: 1    Leader: 1       Replicas: 1     Isr: 1
>         Topic: teste    Partition: 2    Leader: 1       Replicas: 1     Isr: 1
> ~~~

> PARA CONSUMIR UMA MENSAGEM:
> 
> ```kafka-console-consumer --bootstrap-server=localhost:9092 --topic=teste```
> 
> Ao executar o comando acima o consumidor fica ativo e preparado para consumir as mensagens, nada é exibido no console.
> 
> Para consumir as mensagens desde o começo a flag ```--from-beginning``` deve ser passada
>
> Para colocar um consumidor em um grupo a flag ```--group```deve ser passada especificando o nome do grupo. Quando um consumidor está em um group ele vai se encarregar de ler 1 ou mais partições, desde que tenha partições sem consumidor.
> 
> **Exemplo**: 
> 
> ```kafka-console-consumer --bootstrap-server=localhost:9092 --group=x --topic=teste```

> PARA DESCREVER UM CONSUMER GROUP:
> 
> ```kafka-consumer-groups  --bootstrap-server=localhost:9092 --group=x --describe```
> ~~~shell
> kafka-consumer-groups  --bootstrap-server=localhost:9092 --group=x --describe
> # output
> GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID                                       HOST            CLIENT-ID
> x               teste           0          1               1               0               consumer-x-1-005d1526-eaa0-4ee6-8e15-2eea6549f5b5 /172.22.0.3     consumer-x-1
> x               teste           1          2               2               0               consumer-x-1-005d1526-eaa0-4ee6-8e15-2eea6549f5b5 /172.22.0.3     consumer-x-1
> x               teste           2          1               1               0               consumer-x-1-13e5be3b-a996-41ef-83da-77e2e26dd614 /172.22.0.3     consumer-x-1
> ~~~

> PARA PRODUZIR UMA MENSAGEM:
> 
> ```kafka-console-producer --bootstrap-server=localhost:9092 --topic=teste```
> 
> Ao executar o comando acima aparecerá o sinal ```>``` no terminal, a partir dai quando a mensagem for digitada e enviada através do 'enter' esta será consumida.