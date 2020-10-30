Desempate.... Brain spliting

MEMORIA JAVA





Puertos
KUBERNETES -> Opensource y gratuita (Google) |||| OPENSHIFT (Kubernetes+mejoras en la gestion de kubernetes)
                                                    Opensource y gratuito <- REDHAT 
                                                        RedHat Openshift Platform 
                                                            (versión de OPENSHIFT de pago)
    -> Orquestador de Contenedores
    
    Tengo un MONTON de maquinas "fisicas" instalado kubernetes <- cluster kubernetes
        Controlar todas las instalaciones que hago de contenedores en esas máquinas
        
    YO -> Kubernetes: Kubernetes!!! Tengo que desplegar:
        Contenedores de tipo Maestro: 2
        Contenedores de tipo datos casi maestros: 1
        Contenedores de tipo datos: 3->10 según lo veas
        Contenedores de tipo ingesta: 2-4
        Contenedores de tipo coordinacion: 2-4
        
        Servicios (Balanceador de carga):
            Servicio Ingesta    (IP+PUERTO) -> Contenedores de ingesta
            Servicio Busquedas  (IP+PUERTO) -> Contenedores de coordinación
            Servicio Kibana     (IP+PUERTO) -> Contenedores Kibana
            Servicio Cerebro    (IP+PUERTO) -> Contenedores Cerebro
    Kubernetes- > OK!!! Los monto en las que máquinas que gobierno
    
    
^  Instalación de ElasticSearch
------------------------------------------------------------
v  Monitorización y Operación de un cluster de ElasticSearch
    
1º Lenguaje de programación en el que está desarrollado ElasticSearch: JAVA
Particularidades de JAVA                    ¿COBOL?  Compilar -> Traducir nuestro código -> S.O.
                                                     estática

Lenguajes de programación:
    - Compilados:    Cobol, C, C++, PASCAL   -> Mando una carta a un sueco: Traduzco la carta al sueco->sueco
    - Interpretados: Python, Shell (bash)    -> Mando la carta en español... a la espera de que el sueco
                                                  tenga por alli al lado un INTERPRETE... traducción en tiempo real

    Ventaja de leng. interpretado frente a compilado:
        Yo distribuyo lo mismo a todo el mundo
    Ventaja de leng. compilado frente a un interpretado:
        Rapidez... El ordenador entiende directo lo que le he mandado
        
                                                  
    JAVA??? Enjendro !!!!!! PORTABLE + VELOCIDAD Es casi igual a un programa 100% compilado
        - Compilado + Interpretado
            ---> No es contra el SO destino.... SO que se ejecuta dentro de una máquina virtual JVM
            JVM... en tiempo de ejecución interpreta el código para trucirse al SO de destino
            
    Ejecutamos un programa JAVA... ese programa se ejecuta DENTRO de una máquina virtual
        Memoria RAM <--- Maquina virtual <--- programa 
                            5 Gbs               1 Gb     .... Estoy tirando 4 Gbs a la barurita :'(
                            1 Gb                5 Gbs    .... EXPLOSION !!!
            Problema... Ajustar bien la memoria RAM
                Monitorización a nivel de SO.... Me dice la RAM que tiene la Mvirtual
                Pero de esa cúanta se está usando??? A priori NPI... Tengo que buscarme las 
                                                                        mañas para averiguarlo
                                                --- Kibana nos ofrece información de la memoria 
                                                        de elastic dentro de la JVM
                                                        


Que mete Elastic en RAM:
    Cada vez que se quiera hacer una query sobre un índice... el INDICE se sube a RAM desde el disco
    - Si un indice se usa mucho... el indice se mantiene en RAM "indefinidamente"
    - Si un indice se usa poco.... el indice se tira de la RAM a la basura después de haber sido utilizado
    
    BUFFERS A FICHEROS
    Programa ---> Buffer Memoria RAM (el buffer se vacia de vez en cuando... para minimizar las escrituras a disco
        3 Mbs
        Programa ---> Datos... Buffer RAM (100kb)

    Elastic usa MOGOLLON de fichero... necesito mucha RAM para los buffers: 40-50% 
        Los buffers son gestionados por el SO
        La JVM -> 50-60% de RAM del total de la maquina... El resto lo reservo para buffers se SO
    
    
    