Nodos en un cluster de ElasticSearch:
Distintos tipos de nodos:
    - Maestro: 
        Responsabilidad: Coordinar las operaciones del cluster
                            Controlo si los nodos contestan
                            Mueve shards de un nodo a otro
        Cuantos? Mínimo 3 y a partir de ahí impares DESEMPATE
        2 tipos: Maestros con capacidad de ejercer
                 Maestro de mentirijilla... solo pueden votar
    - Datos:
        Son los que almacenan los shards
        Qué operaciones hacen:
            Indexación
            Búsquedas
        Cuantos? Mínimo 2: REDUNDANCIA
    - Ingesta:
        Trabajo: Preprocesar los documentos antes de mandarlos a los nodos de datos
        Cuantos? Mínimo 0, si tengo cúantos? 2: Alta disponibilidad
    - Coordinación:
        Cuantos? Mínimo 0, si tengo cúantos? 2: Alta disponibilidad
        Trabajo: Agrupar resultados de búsquedas, Fusionas búsquedas
        
        
Cluster minimo que vamos a montar:
    Maestros: 2 
    Datos:    2 (1 de ellos es maestros de mentirijilla)

Un cluster tamaño medio:
    Maestros: 2 (activo-pasivo) Activo: El que estña trabajando como maestro.
                                Pasivo: Es el que está de backup por si se 
                                        cae el principal.
    Datos:    4-5 (1 de ellos es maestros de mentirijilla)
    Ingesta: 2
    Coordinacion: 2

Tipos de nodos en elastic:
    Realmente lo que hacemos es decir a cada nodo, cual de esas 4(5) tareas
    pueden realizar:
    
    Para cada nodo:
        Puede ejercer como maestro: SI / NO
        Puede votar al maestro: SI / NO
        Puede ejercer como datos: SI / NO
        Puede ejercer como ingesta: SI / NO
        ---> Puede ejercer como coordinacion: SI / NO (no se especifica)



---------------------------

REPLICAS: 
    - Si hago una búsqueda tengo más potenciales sitios donde buscarlo.
        Eso mejora la escalabilidad? SI ... mejora rendimiento
        
    - Si doy de alta un dato
        Los tiempos, mejoran o empeoran.....
            Hay que mantener todas las replicas.
                Nodos:   Tengo un indice y quiero 2 replicas de los datos
                1 Principal  <- 5ms ---90 %
                2 Replica 1  <- 5ms ---90 % .... se me demore en hacer el grabado
                3 Replica 2  <- 5ms 
            Lo podemos paliar... Desarrollador -> INSERT INDICE <- ACTUALIZADO
                    cuando contesta ES ???
                    En cuanto lo guardes en 1 nodo dame OK
                    En cuanto lo guardes en 2 nodo dame OK
                    Hasta que no lo tengas en todos los posible nodos no me de el OK

----------------------------------------

Cluster de elastic: En un entorno de producción
    Maestros: 2
    Datos:    2 (1 de ellos con decisión a voto)
             +1
        CPU 1 - 75%
        CPU 2 - 75%
        CPU 3 - 55%
             +1 o +O todavia estoy bien
            ESTOY JUGANDO CON FUEGO !!!!!!!!!!!!! Si pienso que tengo HA en esta 
                situación estoy MUY EQUIVOCADO.
        
        El nodo 2 CRUJE... puffff!
            CPU 1 <- 100%
            CPU 3 <- 100%
            Y aun así me falta capacidad de trabajo.... 
            ---> Nodo 1 ... puf !!!!!
            ------> Nodo 2  ... MEGA PUFFF !!!!
            CAIDA EN CASCADA !!!!
---------------------------------------
Indice A 10 particiones
Indice B 10 particiones
Indice C 10 particiones
    Datos 1:
        CPU: 20%
        HDD: 48%
        RAM: 4Gbs - 16Gb
            Indice A . 10 Primarias
            Indice B . 5 replicas        +++++ 5 replicas
            Indice C . 5 replicas        +++++ 5 replicas
    Datos 2:
        CPU: 20%
        HDD: 45%
        RAM: 4Gbs - 16Gb
            Indice A . 5 replicas         ++++ 5 replicas 4Gbs
            Indice B . 10 primarias
            Indice C . 5 replicas         ++++ 5 replicas 4Gbs
            PUEDO ESTAR JUGANDO CON FUEGO !!!!!!!!!!!!! Si pienso que tengo HA en esta 
                situación puedo estar MUY EQUIVOCADO.  Que pasa con los HHD
            Indices 20 Indices... 200Mbs Copias
    Datos 3:
        RAM: 4Gbs - 16Gb
        CPU: 20%
        HDD: 2%
---            Indice A . 5 replicas
---            Indice B . 5 replicas
---            Indice C . 10 primarias
   
    Ni de coña!
        Datos 3 cruje!