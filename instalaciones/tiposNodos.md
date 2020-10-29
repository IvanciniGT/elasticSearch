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
        