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