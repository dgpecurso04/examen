# examen
examen

#ejecutar en linea de comandos para correr el servidor vertex desde un docker
# #RUTA_EXTERNA = ruta del proyecto donde tienes examen#
docker run -d -p 8081:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample 
-e PBA=server8081 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

#Ingresar la direccion en el navegador
http://localhost:8081/calculadora/suma?numA=3&numB=2
http://localhost:8081/calculadora/resta?numA=3&numB=2
http://localhost:8081/calculadora/mult?numA=3&numB=2
http://localhost:8081/calculadora/div?numA=3&numB=2

#PASOS PARA BALANCEAR 6 CONTENEDORES
#AGREGAR
docker run -d -p 8081:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8081 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

docker run -d -p 8082:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8082 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

docker run -d -p 8083:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8083 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

docker run -d -p 8084:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8084 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

docker run -d -p 8085:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8085 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

docker run -d -p 8086:8080 -v #RUTA_EXTERNA#/examen:/vertx-sample
-e PBA=server8086 gustavoarellano/jdk18 java -jar /vertx-sample/target/sample-1.0-SNAPSHOT-fat.jar

#agregar al archivo nano /etc/default/haproxy
CONFIG="/etc/haproxy/haproxy.cfg"
ENABLED=1

#agregar al archivo nano /etc/haproxy/haproxy.cfg 

frontend www
        bind 0.0.0.0:9090
        default_backend site-backend

backend site-backend
        mode http
        balance roundrobin
        stats enable
        stats uri /haproxy?stats
        server lamp1 localhost:8081 check
        server lamp2 localhost:8082 check
        server lamp3 localhost:8083 check
	server lamp4 localhost:8084 check
	server lamp5 localhost:8085 check
	server lamp6 localhost:8086 check
#ejecutar la ip en el navegador

http://localhost:9090/calculadora/suma?numA=3&numB=2
http://localhost:9090/calculadora/resta?numA=3&numB=2
http://localhost:9090/calculadora/mult?numA=3&numB=2
http://localhost:9090/calculadora/div?numA=3&numB=2

