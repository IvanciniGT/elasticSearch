AMAZON: 
    Es una empresa, que tiene:
        - Una página web que vende productos (pilas, camiseta, ordenador)
        - Otra página web que ofrece servicios a empresas: AWS
            Amazon web services
            

CREADO UN ORDENADOR EN AMAZON AWS ???
    4 cpus, 16Gbs <- SO ??? Ubuntu (Linux)


UNIX ERA un SO <- AT&T (de pago)
--------------------------------
Se hicieron DOS especificacion de como funcionaba ese sistema operativo:
    UNIX    <- Como funciona el SO por dentro
    POSIX   <- Como interactuaba ese SO con aplicaciones externas
        --->> Se gestionan por el mismo grupo de gente: AUSTIN GROUP
        
Hay empresas que hacen Sistemas Operativos que siguen la especificación de UNIX:
    IBM    <----- AIX      -> UNIX ®
    ORACLE <----- SOLARIS  -> UNIX ®
    HP     <----- HP-UX    -> UNIX ®
    Apple  <----- MacOS    -> UNIX ®
Todos esos sistemas operativos han pasado una prueba para asegurarse que cumple a 
rajatabla la especificacion de UNIX. 
ESTA PRUEBA QUE HAN PASADO ESTOS SISTEMAS NO ES GRATIS... cuesta pasta

Hay gente que decidió hacer un S.O. según la especificación de UNIX,
pero que nunca se sometieron a la prueba pertinente:
-> BSD (Berkley Software Distribution) SEGUIMO LA SPEC: UNIX.... SOMOS UNIX
        ----> DENUNCIA AL CANTO... DE AT&T... BSD -> BASURA
        BSD -> FreeBSD (Routers)
-> GNU <- Terminal, Editores de texto, juego, programa ventanas, XXXX<->(KERNEL)
    GNU is not UNIX 
-> Linus Torwalds ---- Me aburroo... voy a este finde un KERNEL DE SO
    ----> 7 Millones de lineas de codigo ----> Kernel SO <- Cumplia la espec UNIX
            Soy un Kernel TIPO unix
----> Linus <- Kernel                 |
      GNU   <- Todo menos un kernel   | Sistema operativo GNU/Linux
                                                          70%  25%
        Linus' UNIX
        
        
    Me gustan las librerias de GNU, me gusta el kernel de LINUX, pero...
    Distribuciones de linux
        Yo quiero además estos programas.XXXXXX     
        Yo quiero además estos otros programas.XYYYYYYXXXXX
        Yo quiero además estos otros programas.ZZZZZ
    
    DEBIAN  -> UBUNTU
    REDHAT  -> FEDORA, CENTOS, OracleLinux
    SUSE
    
    ANDROID <- Kernel LINUS + 
                librerias que no son de GNU, sino otros realizadas por GOOGLE
    
    
----------------------
Microsoft-> Windows Server   <- Kernel NT -> POSIX
Microsoft-> Windows 10       <- 2 Kernels de SO:
    - Kernel NT (new technology)
    - Linux     <---- PARA PODER EJECUTAR CONTENEDORES DE 
    

Clouds <- El conjunto de todos los servicios que ofrece una emrpesa a través de INTERNET

AMAZON:    AWS<- Es el cloud de Amazon
MICROSOFT: AZURE
GOOGLE:    GOOGLE CLOUD
ORACLE:    ORACLE CLOUD



Cloud AWS:
    Creado una máquina 4 cores y 16Gbs RAM + UBUNTU (distrib linux)
                                                V
                                                Contenedor <- Tomcat 
                                                (como si fuera otro ordenador)

    Cómo me comunico yo con un ordenador???? 
        Interfaz de comandos <- Terminal interactiva <<<<<<<
        Interfaz gráfica     <- Botones, ventanas 

    Cuantas terminales de comandos puedo abrir contra un ordenador a la vez?
        TODAS LAS QUE ME DE LA GANA
        
        
        
        










Programa X
    - Como me comunico con mi programa?
        Interfaz gráfica <- APLICACION
                                WORD, EXCEL --- 
                                NAVEGADOR WEB
        ENTRADA Y SALIDA <- CUALQUIERA DE LOS COMADOS QUE EJECUTAMOS EN UNA TERMINAL
                                COMANDOS
                                SCRIPT
        Un servicio es un programa pensado para ser utilizado por otro programa                        
        MENSAJES            SERVICIOS, DAEMON
            CANAL DE COMUNICACION
                RED----> PUERTO
        
        TOMCAT ??? Servidor de aplicaciones: Servicio <- 8080
    
Para saber en una máquina LINUX cuales son los puertos que está en uso?
netstat -lnt

NIC ? Netword Card Interface = TARJETA DE RED ??? 
    LAN (RJ45) Cable
    Wifi

NIC - Tarjeta de RED - VIRTUALIZACION -> Una UNICA tarjeta de RED puede presentarse al SO
                                         Como si en realizad fueran 100 tarjetas de red
 ^    
Interfaz de RED ? Mecanismo por el que nos conectamos a una RED



                         Internet
-------------------------------------------------------------------------
|        |        |         |         |         |       |               |
Router                                                                  Router AMAZON
|                                                                       |
------                                                                  ----------------------
|  |                                                                    |       |      |     |
| Movil                                                             Ubuntu_Ivan
|                                                             ( Interfaz de red: RED DE AMAZON <- 172.31.5.19 )
Ivan    Luis     Hortensia  Pilar    Juan     Olga     Pol              

UbuntuIvan:
    - Interfaz de red: RED DE AMAZON <- 172.31.5.19
    - Interfaz de red: Local         <- 127.0.0.X (127.0.0.1 ~ localhost ~ home)
    - 
Como puedo preguntar a una máquina LINUX por sus interfaces de RED y sus IPS
    ifconfig <- (deprecated) <- ip a
    ipconfig <- WINDOWS


There is no place like 127.0.0.1

  INTERNET
    |
  RED DE AMAZON
    |
172.31.5.18
    |
UBUNTU_IVAN ------ local: 127.0.0.1
    *:8080 >>>>>>> 172.17.0.2:8080   MAPEO DE PUERTOS
    (docker)
        |
    172.17.0.1
        |
        ------------------------------ 172.17.X.X
        |               |            |
    172.17.0.2      172.17.0.3     172.17.0.4
        |               |            |
        C1              C2          C3
        Tomcat

Direcciones locales siempre empiezan por 0.0.X.X o por 127.0.X.X
Direcciones de red privadas: 192.168.X.X     172.X.X.X



Walki-talkies                                                       TOMCAT
    Emisor: Persona                                                     Programa: curl (call url)
    Receptor: Persona                                                   Tomcat
    Canal: Walkitalkies + ondas radio... aire                           Red / Interfaz de RED / IP
        Walk... Los tengo que sintonizar en la misma frecuencia             Puerto
    Mensaje: Palabras que nos decimos                                   Parte de la URL
    Protocolo: Corto/Cambio/Apreto el botón                             HTTP
    
URL ????
    Uniform Resource Locator
    protocolo :// destino(Red) : puerto / contexto ? queryString
    
    http://xataka.com
    http://xataka.com/
    http://xataka.com:80/
    
        protocolo: http
        destino:   xataka.com
        puerto:    80
        contextp:  /
        queryString: nada
    
    
    https://www.google.es/search?sxsrf=ALeKk01sfas-foKuJKS4FuXMiUyIpFRHJg%3A1603823425375&source=hp&ei=QWeYX6-NEpGua8vLu9gG&q=cvxbxcvbxv&oq=cvxbxcvbxv&gs_lcp=CgZwc3ktYWIQAzoHCCMQ6gIQJzoECCMQJzoECAAQQzoICAAQsQMQgwE6BQgAELEDOgIIADoHCAAQsQMQCjoECAAQCjoGCAAQChATOgQIABANOgYIABANEB5QoCRYrilg-CpoAnAAeAGAAXyIAZMHkgEDNy4zmAEAoAEBqgEHZ3dzLXdperABCg&sclient=psy-ab&ved=0ahUKEwjvsbDss9XsAhUR1xoKHcvlDmsQ4dUDCAk&uact=5