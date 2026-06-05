# Kafka

## Componentes

- **Tópicos:** unidades lógicas de almacenamiento de mensajes en Kafka. Cada tópico mantiene una secuencia ordenada de registros, dividida en particiones para escalabilidad y replicación.

- **Producers (writers):** aplicaciones o servicios que publican mensajes en los tópicos. Los productores envían datos a Kafka, eligiendo la partición adecuada según la clave del mensaje o la estrategia de particionamiento.

- **Consumers:** aplicaciones o servicios que leen mensajes de los tópicos. Los consumidores pertenecen a grupos de consumidores y Kafka distribuye las particiones entre los miembros del grupo para procesar los mensajes de forma paralela.

- **Server:**

- **Server:**

- **Clientes:**

- **Broker:**

- **Partition:**

### Producers

kafka-console-producer.sh

se encuentra en la carpera `bin/` junto a otras herramientas de kafka

Opciones Requeridas

- `--bootstrap-server`: especidifica con qué sistema kafka debe comunicarse el valor por defecto es localhost-9092

- `--topic`: temas

**Ejemplos:**

```bash
bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic testing
bin/kafka-console-producer.sh --topic phishing-sites --bootstrap-server localhost:9092
>este es mi oprimer mensaje
echo "This is a test message" | bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic phishing-sites
```

### Consumers

kafka-console-consumer.sh

se encuentra en la carpera `bin/` junto a otras herramientas de kafka

Opciones Requeridas

- `--bootstrap-server`: especidifica con qué sistema kafka debe comunicarse el valor por defecto es localhost-9092

- `--topic`: temas

- `--from-beginning`:

- `--max-messages <number>`:

> [!WARNING]
> Si el numero maximo de mensaje no se alcanza se quedara esperando hasta que se cumpla

**Ejemplos:**

```bash
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testing
bin/kafka-console-consumer.sh --topic phishing-sites --bootstrap-server localhost:9092 --from-beginning
"2024-03-02 10:54:04","5.50","http://bafybeicyoou3q7k5bml4hx2cqyi7ytj76vckg4hfeuvxbwxh3uw3qlhwwu.ipfs.cf-ipfs.com","104.17.96.13"
"2024-03-02 10:54:00","2.90","http://aprackspace.serveusers.com/","157.230.23.237"
"2024-03-02 10:53:59","1.40","http://aprackspace.serveusers.com","157.230.23.237"
"2024-03-02 10:53:58","3.40","http://aolupdatess2234.weeblysite.com/","172.66.0.60"
"2024-03-02 10:53:56","1.90","http://aolupdatess2234.weeblysite.com","162.159.140.60"
"2024-03-02 10:53:55","2.90","http://aaqpc.blogspot.md/","2607:f8b0:4006:81c::2001"
"2024-03-02 10:53:54","1.40","http://aaqpc.blogspot.md","142.250.176.193"
"2024-03-02 10:53:39","1.80","http://2zhzdm0lwrjmdqtngi.pages.dev/","2606:4700:310c::ac42:2c7c"
"2024-03-02 10:53:36","1.80","http://2zhzdm0lwrjmdqtngi.pages.dev","2606:4700:310c::ac42:2c7c"
"2024-03-02 10:53:33","2.00","http://20.199.80.76/br/safra/Cj0KCQjwj7CZBhDHARIsAPPWv3dBKLTij9FhkvHdG7H0DVWgoR04TYQmSOtI/Pt-br/index.html","20.199.80.76"
bin/kafka-console-consumer.sh --topic phishing-sites --bootstrap-server localhost:9092 --from-beginning --max-messages 3
```

### Topics

kafka-topics.sh

se encuentra en la carpera `bin/` junto a otras herramientas de kafka

Opciones Requeridas

- `--bootstrap-server`: especidifica con qué sistema kafka debe comunicarse el valor por defecto es localhost-9092

- `--topic`: temas

- `--create`:

Opcionales

- `--replication-factor`: Define el factor de replicación  del tema.

- `--partitions`: Especifica el numero de particiones manualmente.

- `--describe`: Nos da detalles sobre la configuraciones del tema.

- `--delete`: Elimnará el tema de un servidor/cluster de Kafka

> [!DANGER]
> Esto también eliminara todos los mensajes de los temas



**Ejemplos:**

```bash
bin/kafka-topics.sh --bootstrap-server localhost:9092 \
--topic orders --create

# Especificando las particiones y el factor de replicación

bin\kafka-topics.sh --bootstrap-server localhost:9092 \
--topic orders --create --replication-factor 3 \
--partitions 3 

# Obtener info del tema
bin/kafka-topics.sh --bootstrap-server localhost:9092 \
--topic orders --describe

# Eliminar el tema
bin/kafka-topics.sh --bootstrap-server localhost:9092 \
--topic orders --delete

bin/kafka-topics.sh --bootstrap-server localhost:9092 \
--topic phishing-sites --delete

```


## Comandos

```bash
bin/kafka-topics.sh --help

This tool helps to create, delete, describe, or change a topic.
Option                                   Description                            
------                                   -----------                            
--alter                                  Alter the number of partitions and     
                                           replica assignment. Update the       
                                           configuration of an existing topic   
                                           via --alter is no longer supported   
                                           here (the kafka-configs CLI supports 
                                           altering topic configs with a --     
                                           bootstrap-server option).            
--at-min-isr-partitions                  if set when describing topics, only    
                                           show partitions whose isr count is   
                                           equal to the configured minimum.     
--bootstrap-server <String: server to    REQUIRED: The Kafka server to connect  
  connect to>                              to.                                  
--command-config <String: command        Property file containing configs to be 
  config property file>                    passed to Admin Client. This is used 
                                           only with --bootstrap-server option  
                                           for describing and altering broker   
                                           configs.                             
--config <String: name=value>            A topic configuration override for the 
                                           topic being created or altered. The  
                                           following is a list of valid         
                                           configurations:                      
                                                cleanup.policy                        
                                                compression.type                      
                                                delete.retention.ms                   
                                                file.delete.delay.ms                  
                                                flush.messages                        
                                                flush.ms                              
                                                follower.replication.throttled.       
                                           replicas                             
                                                index.interval.bytes                  
                                                leader.replication.throttled.replicas 
                                                local.retention.bytes                 
                                                local.retention.ms                    
                                                max.compaction.lag.ms                 
                                                max.message.bytes                     
                                                message.downconversion.enable         
                                                message.format.version                
                                                message.timestamp.after.max.ms        
                                                message.timestamp.before.max.ms       
                                                message.timestamp.difference.max.ms   
                                                message.timestamp.type                
                                                min.cleanable.dirty.ratio             
                                                min.compaction.lag.ms                 
                                                min.insync.replicas                   
                                                preallocate                           
                                                remote.storage.enable                 
                                                retention.bytes                       
                                                retention.ms                          
                                                segment.bytes                         
                                                segment.index.bytes                   
                                                segment.jitter.ms                     
                                                segment.ms                            
                                                unclean.leader.election.enable        
                                         See the Kafka documentation for full   
                                           details on the topic configs. It is  
                                           supported only in combination with --
                                           create if --bootstrap-server option  
                                           is used (the kafka-configs CLI       
                                           supports altering topic configs with 
                                           a --bootstrap-server option).        
--create                                 Create a new topic.                    
--delete                                 Delete a topic                         
--delete-config <String: name>           A topic configuration override to be   
                                           removed for an existing topic (see   
                                           the list of configurations under the 
                                           --config option). Not supported with 
                                           the --bootstrap-server option.       
--describe                               List details for the given topics.     
--exclude-internal                       exclude internal topics when running   
                                           list or describe command. The        
                                           internal topics will be listed by    
                                           default                              
--help                                   Print usage information.               
--if-exists                              if set when altering or deleting or    
                                           describing topics, the action will   
                                           only execute if the topic exists.    
--if-not-exists                          if set when creating topics, the       
                                           action will only execute if the      
                                           topic does not already exist.        
--list                                   List all available topics.             
--partitions <Integer: # of partitions>  The number of partitions for the topic 
                                           being created or altered (WARNING:   
                                           If partitions are increased for a    
                                           topic that has a key, the partition  
                                           logic or ordering of the messages    
                                           will be affected). If not supplied   
                                           for create, defaults to the cluster  
                                           default.                             
--replica-assignment <String:            A list of manual partition-to-broker   
  broker_id_for_part1_replica1 :           assignments for the topic being      
  broker_id_for_part1_replica2 ,           created or altered.                  
  broker_id_for_part2_replica1 :                                                
  broker_id_for_part2_replica2 , ...>                                           
--replication-factor <Integer:           The replication factor for each        
  replication factor>                      partition in the topic being         
                                           created. If not supplied, defaults   
                                           to the cluster default.              
--topic <String: topic>                  The topic to create, alter, describe   
                                           or delete. It also accepts a regular 
                                           expression, except for --create      
                                           option. Put topic name in double     
                                           quotes and use the '\' prefix to     
                                           escape regular expression symbols; e.
                                           g. "test\.topic".                    
--topic-id <String: topic-id>            The topic-id to describe.This is used  
                                           only with --bootstrap-server option  
                                           for describing topics.               
--topics-with-overrides                  if set when describing topics, only    
                                           show topics that have overridden     
                                           configs                              
--unavailable-partitions                 if set when describing topics, only    
                                           show partitions whose leader is not  
                                           available                            
--under-min-isr-partitions               if set when describing topics, only    
                                           show partitions whose isr count is   
                                           less than the configured minimum.    
--under-replicated-partitions            if set when describing topics, only    
                                           show under replicated partitions     
--version                                Display Kafka version.    
```

```bash 
bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
cleaned-devices
compromised-systems
known-exploits
phishing-sites
```

```bash
/home/repl/check_broker.sh
Broker count: 1
```

> [!IMPORTANT]
> Recordar que kafka tiene un tolerancia de caidas de -1 entonces en este caso 1 - 1 = 0 por lo cual si se cae el servidor se perderan todos los datos. 

## Enfoque con ZooKeeper

`config/zookeeper.properties`
`config/server.properties`

`bin/zookeeper-server-start.sh config/zookeeper.properties`

`bin/kafka-server-start.sh config/server.properties`

`bin/kafka-server-stop.sh config/server.properties`

`bin/zookeeper-server-stop.sh config/zookeeper.properties`

## Troubleshooting

`ps ac | grep kafka`: verifica si hay un servicio llamado kafka en ejecución.

`netstat -tlpn | grep 9092`: verifica que se escuchando en el puerto 9092