HTTP
Enviais datos a un servidor web

Navegador  -----> Servidor WEB
            url
            
    protocolo://servidor:puerto/contexto?parametros
    http://nodo1:9200/
    
        Protocolo: http
        servidor: nodo1
        puerto: 9200
        contexto: /
    
    Adicional a la URL : SOLO SIRVE PARA IDENTIFICAR DONDE ME CONECTO
    Nos conectamos por HTTP
        Me permite es enviar ficheros de caracteres entre un ordenador y otro
        Esos ficheros se guardan dentro de una caja
        Y a la caja se le pone una pegatina fuera con una serie de metadatos
        
        METODO: GET   <- Pedir cosas al servidor
                POST  -> Mandar cosas al servidor
                DELETE 
                PUT
                HEAD
        ----------
        STATUS: Estado de la respuesta:
                2XX  ----> Todo ha ido bien
                3XX  ----> Te he mandado a otro sitio (redireccion)
                4XX  ----> Errores en el cliente
                5XX  ----> Errores en el servidor
                
Llamada a una URL: Contexto: Donde quiero operar
        Metodo: GET, POST, PUT, DELETE, HEAD
        Fichero---> Opcionalmente (JSON)
        
Elastic contesta:
        Fichero JSON
        Codigo de estado: 2XX, 3XX, 4XX, 5XX
        
URL: http://nodo1:9200/
    Metodo: GET
    Fichero: NADA

    Respuesta: Fichero JSON: Estoy listo
    


    
Elastic: Puertos:
    9200. -> Que los clientes se conecten
    9300. -> Comunicarse entre los nodos de elastic

Kibana:
    5601. -> Que los clientes se conecten
    ---> Tiene que conectarse con ElasticSearch --> 9200
            Con quien conecto a kibana ? Puede atacar a cualquier nodo

Cerebro:
    9000  -> Que los clientes se conecten... Un nodo de un elastic.... 
    
    
    
    
-----------------------------------------------------------------------

Protocolo usando para comunicación de elastic con el exterior ????
    HTTP -> TCP/IP

Protocolo usando para comunicación entre los nodos de elastic ????
    HTTP -> TPC/IP
    
Creeis que podríamos mejorar la seguridad en las comunicaciones?
SI. Como? Usando el protocolo: HTTPS
Donde? 
    a) Desde elastic hasta el exterior        <<<<<<<<<
    b) Entre los propios nodos de elastic     <<<<<<<<<
>>>>>>    c) Ambas respuestas son válidas           <<<<<<<<<<<<<

¿Que necesitamos??        
    CADA NODO DEL CLUSTER:
        Generar claves publicas / privadas  
        Su propio certificado
------------------------------------------------------------------
Toda la configuración de elasticsearch se realiza mediante MODULOS
NETWORK: Define como son las comunicaciones de elasticsearch
    características genéricas configuración
    HTTP:       características propias de la comunicación 
                de elastic con el exterior
            - Puerto de comunicación con el exterior
            - Si quiero SSL con el exterior
                    Secure socker layer -> HTTPS (HTTP + SSL)
    TRANSPORT:  características propias de la comunicación
                entre los nodos del cluster
            - Puerto de comunicación entre nodos
            - Si quiero SSL entre los nodos
                    Secure socker layer -> HTTPS (HTTP + SSL)
------------------------------------------------------------------
ELASTICSEARCH: TIPO DE LICENCIA: Apache (Opensource)
¿Cuantas instalaciones de ES Opensource 
        pensais que existen en el mundo?    NINGUNA (3)

Quien hace elasticSearch? Elastic Co.
    Elasticsearch -> Opensource (NO SE LE PUEDE ACTIVAR HTTPS)
    
XPACK -> Librerias desarrolladas por la gente de ELASTICSEARCH 
            QUE NO SON OPENSOURCE
    Esas librerias amplian la funcionalidad de ELASTICSEARCH
        XPACK <- BASIC (Ofrece toda la capa de seguridad)
                    gratis
    

------------------------------------------------------------------
    
HTTP + CAPA SEGURIDAD EXTRA => HTTPS
    - Man in the middle - ESPIAR... COTILLEAR
        Pinchar la linea ... Esconderme detras del muro
        Frustrar mediante encriptación
    - Phishing - Suplantación de identidad
        Frustrar con la ayuda de certificados
    
Encriptar la información

    JQNC +2
    IPMB +1
    ||||
    VVVV
    HOLA
    
    Algoritmo: Corrido de letras según el ordel del alfabeto
                Clave: 1
                Clave: 2
    
Algoritmos de encripción:
    - Clave simétrica:
        Con la misma clave encrito y desencripto
    - Clave asimétrica
    Existen 2 claves que se generan en pareja.
        1 clave sirve para encriptar, pero no desencripta
            Clave PRIVADA
        1 clave sirve para desencriptar, no encripta
            Clave PUBLICA

HTTP: Se usan tanto claves simetricas como asimetricas
        -> A traves de un algoritmo de clave asimetricas
            Se comparte una clave simetrica
            Que es la que se utilzia a partir de ese momento
Los algoritmos de clave simetrica son MUCHO MAS RAPIDOS

En un momento dado, (al inicio) se usa:
    clave asimetrica + PRIVADA + PUBLICA

---------------------------------------------------------------

Iván:   DNI                 <- Policia Nacional
        Carnet de conducir  <- Guardia Civil
        Carnet de la biblioteca de mi barrio
        Policia Nacional -> 
            Los carnet emitidos por la biblioteca del barrio de Ivan
            son de nuestra TOTAL confianza
        
        Normativa: Como debe ser el carnet (datos debe incluir)
        Normativa: Como se entrega el carnet a una nueva persona
        
Confianza en si soy o no Iván, depende de vuestra confianza 
    en el documento que os presento.

CERTIFICADO
    -> Quien es el poseedor: NOMBRE DE UN SERVIDOR ( & IP )
                             CLAVE PUBLICA 
    -> Alguien que respalde el certificado: 
        ENTIDAD CERTIFICADORA (CA)
        
        
¿Cuanta gente necesito para administrar un ORACLE?
    Instalación
    Mantenimiento ? Depende <<<<<<<

Seguros REALE Seguros
    Oracle -> 512 HDD
    2 personas Backup and Recovery ORACLE 
    
Indices: 
    MAPPINGS <---- Desarrollador
    SETTINGS <---- Administrador

Nominas : 2-27  NI EL TATO
          28-1  TODO EL MUNDO 
                    -> CLUSTER 
                        -> BALANCEADORES
                        -> MONITORIZACION HEARTBEATS ARRIBA O ABAJO 

        Backups CALIENTE FRIO .. INCREMENTABLE... FULL 







