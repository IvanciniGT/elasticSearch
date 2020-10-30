
Cluster ElasticSearch
    Nodo1
    
    Nodo2
    
    Nodo3
    
Cargar un documento dentro de ElasticSearch ---> JSON
Donde se carga el documento ----> Indice <--- Particiones primarias * Replicas
                                              Shards  <---- Lucenes
{
    'nombre': 'Iván Osuna Ayuste',
    'edad': 42,
    'email': 'ivan@correo.com',
    'poblacion': 'Colmenar viejo',
    'ip': '87.23.54.12',
    'posicion': {
        'lat': 982367638628,
        'lon': 127887687678
    }
}
--------> Lucene
    1 - Indexar cada campo del documento:
        nombre:         "Iván Osuna Ayuste"
            tokenizar:   Iván - Osuna - Ayuste
            caracteres:  iván - osuna - ayuste
            caracteres:  ivan - osuna - ayuste
            filtros:     ivan -   x   - ayuste  (stopwords: osuna)
            genera el indice invertido:
                ivan   - posición 1
                ayuste - posición 3
    2 - Guardar una copia del documento <- OPCIONAL (Es por defecto que si)
Tipos de datos:
    keyword <- Token que no se procesa... se indexa tal cual
                DNI, código postal
    text    <- Texto que se procesa para búsquedas fulltext
                Nombre completo , Dirección
                    Avenida de Cristobal Colón
                        Colon
                        colon
                        Avenida cristobal colon
                        avda cristobal colon
    ip
        
    geo_point
Elastic:
    En los documentos(JSON) de el indice X, los campos que debes tratar son:
        nombre:   Es un campo de tipo text
        ip:       Es un campo de tipo IP
        posicion: Es un campo de tipo geo_point
    Estas reglas, donde decimos los tipos de campo 
        y el tratamiento que queremos para cada campo
        ---> MAPPING

---------------------------
ElasticSearch, ¿Quiere trabajar con muchos indices o con pocos?
BANCO:
Transferencias bancarias que se hacen a lo largo del día
{
    ordenante
    destinatario
    concepto
    importe
}
Un INDICE con TODAS las transferencias habidas y por haber?
Un INDICE para cada MES?
**** Un INDICE para cada DIA? <- Ficheros más pequeños.... Los puedo congelar
    - CONGELAR: No se pueden hacer cambios de ningún tipo <--- 
    - COMPACTAR: Junta todos los ficheros en uno <--- más velocidad
    -

Ficheros de los índices?
    Como guarda los datos? Tiene muchos huecos por ahi en medio... 
    por si acaso le hace falta

--- FICHERO DE INDICE ---
1 Estela
2 
3
4 Isabel
5 
6 Luis
7
8 Maria Pilar
9
10 Olga
11
12
13 Pol
14
15 Santiago
16 
------------------------
Todas las transferencias del 2 de nov de 2020
    GET /transferencias20201102/_search
Todas las transferencias de nov de 2020
    GET /transferencias20201101/_search
    GET /transferencias20201102/_search
    ...
    GET /transferencias20201130/_search
Elastc permite caracteres comodín
    GET /transferencias2020*/_search

ALIAS

/TransferenciasInternacionales20201101
    /OperacionesTI20201101
/TransferenciasInternacionales20201102
    /OperacionesTI20201102

/TransferenciasNacionales20201101
    /OperacionesTN20201101
/TransferenciasNacionales20201102
    /OperacionesTN20201102

/MovimientosCuenta20201101
    /OperacionesM20201101
/MovimientosCuenta20201102
    /OperacionesM20201102

/CargosTarjeta20201101
    /OperacionesC20201101
/CargosTarjeta20201102
    /OperacionesC20201102

/Contratos20201101

// Transferencias, Movimentos, Cargos... pero no quiero contratos
GET /Operaciones*202011*/_search?dni: 93857183A



ID: 112
{
  "titulo": "Una noche en la Opera",
  "artista": "Queen",
  "fecha": 1975,
  "ip": "192.168.1.32",
  "posicion": {
    "lat":12783681723,
    "lon":1398712873
  },
  "población": "Colmenar viejo",
  "canciones": [ "cancion 1", "cancion2", "cancion3" ]
}
---------->
'noche'  aparece en el titulo del documento 112, en la posición 2
'opera'  aparece en el titulo del documento 112, en la posición 5
'queen'  aparece en el artista del documento 112, en la posición 1
'cancion 1' aparece en el primer elemento dentro de canciones del documento 112



titulo: Noche+Concierto
fecha: 1975

1er - Concierto de la noche blanca: 1975
2er - Concierto de la noche negra: 1978
3er - Concierto del dia gris: 2002


Busquedas: se calcula un score
Filtros <--- SI O NO --- No se calcula score

----------------------------------------------

doc1: Hola ... en un rato hacemos el examen.... que miedo uuhhh!!!!
doc2: Hola ... en un rato seguro aprobais el examen.... ;)

--> Indice
termino        ubicación
hola        -> doc 1: titulo: pos 3     doc 2: concepto: 17
rato        -> doc 1 doc 2
hacemos     -> doc 1
examen      -> doc 1 doc 2
miedo       -> doc 1
seguro      -> doc 2
aprobais    -> doc2


0              0
En las primeras cargas ... irían creciendo ambos, pero de manera no muy dirferente
+ tiempo
+ tiempo
En un momento dado SOLO deben crecer las ubicaciones... los terminos casi no crecerán

Operaciones en un banco asociadas a un DNI
DNI: 100.000.000 millones
DNI: 1000000000000000000000 millones


PARTICIONES DEL INDICE
Particion 1 <--- Operaciones realizadas los martes... En los ficheros de la Part 1
    100000000 Millones de DNIS pueden estar en todas las particiones
    DNI
Particion 2 <--- Operaciones realizadas otros dias... En los ficheros de la Part 2
    100000000 Millones de DNIS pueden estar en todas las particiones

Lo que ocupan los datos del indice: 
    Terminos :    100Mb
    Ubicaciones : 500Mb
                ---------
                  600 Mb ---> Fichero ----> RAM
2 particiones:
    Particion 1: 
        Terminos :    80Mb
        Ubicaciones : 100Mb
                     ------
                      200Mb
    Particion 2: 
        Terminos :    80Mb
        Ubicaciones : 100Mb
    Particion 3: 
        Terminos :    80Mb
        Ubicaciones : 100Mb
    Particion 4: 
        Terminos :    80Mb
        Ubicaciones : 100Mb
    Particion 5: 
        Terminos :    80Mb
        Ubicaciones : 100Mb
        
                    ---------
                     1000 Mb ---> Fichero ----> RAM
    
    

---------------------------
DNI: 12345L                 Keyword
Importe: 534                Number
Concepto: Compra en Amazon  TEXT
Fechas: 10 Enero de 2019    Fecha
Hora: 15:27                 Hora
Estado: Finalziada          Keyword
---------------------
S1 .----> DNI <50000
Compra
Amazon
Enero
Finalizado
S1 .----> DNI >50000
Compra  
Amazon
Enero
Finalizado