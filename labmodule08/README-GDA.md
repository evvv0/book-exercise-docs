# Gateway Device Application (Connected Devices)

## Lab Module 08

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Mi implementación crea e integra un servidor CoAP utilizando la biblioteca Californium en una clase llamada CoapServerGateway, permitiendo la recepción y manejo de mensajes CoAP dentro del sistema. Este servidor se enlaza con la clase DeviceDataManager, lo que permite gestionar y procesar los datos recibidos a través de CoAP como parte de la lógica general de la aplicación. Además, he creado dos manejadores de recursos llamados UpdateSystemPerformanceResourceHandler y UpdateTelemetryResourceHandler, que extienden de CoapResource y permiten que el cliente (CDA) envíe solicitudes PUT con datos JSON para actualizar la información de rendimiento del sistema y los datos de telemetría. Esta arquitectura facilita la recepción de datos IoT de forma estructurada y segura, habilitando la interoperabilidad basada en el protocolo CoAP.

Adicionalmente, he implementado un nuevo manejador de recursos llamado GetActuatorCommandResourceHandler, que está basado en GenericCoapResourceHandler y está diseñado para permitir que el GDA notifique al CDA sobre comandos de actuación mediante la especificación CoAP OBSERVE. Este manejador también extiende de CoapResource y, a través de la implementación de la interfaz IActuatorDataListener, es capaz de recibir actualizaciones de datos de actuadores desde DeviceDataManager y notificar a los clientes conectados mediante la función changed(). Para ello, se ha actualizado DeviceDataManager para permitir el registro de un IActuatorDataListener nombrado, integrando la lógica en el método handleIncomingDataAnalysis() para redirigir los datos de actuación al listener registrado. También se ha ampliado la lógica de CoapServerGateway para soportar tanto la creación interna como la adición externa de recursos CoAP, con métodos como addResource() y createAndAddResourceChain(), facilitando así la construcción jerárquica de los recursos del servidor y su integración flexible en tiempo de ejecución.

How does your implementation work?
La clase CoapServerGateway instancia un servidor CoAP utilizando la biblioteca Californium y lo configura con un listener para recibir mensajes de datos. Al inicializar el servidor, se pueden registrar recursos CoAP específicos mediante métodos personalizados o externos. La clase implementa métodos para iniciar y detener el servidor, asegurando que los endpoints estén correctamente configurados con trazadores de mensajes para depuración. Este servidor se integra dentro de DeviceDataManager, que, dependiendo de una configuración booleana (enableCoapServer), inicializa y activa el servidor durante el ciclo de vida de la aplicación, permitiendo así la comunicación mediante el protocolo CoAP en la infraestructura IoT del sistema.
Los manejadores UpdateSystemPerformanceResourceHandler y UpdateTelemetryResourceHandler gestionan solicitudes PUT, POST, DELETE y GET. El método handlePUT() acepta una carga útil JSON, la convierte en una instancia de SystemPerformanceData o SensorData, y la reenvía a DeviceDataManager a través de un IDataMessageListener. Además, los métodos GET, POST y DELETE implementan funcionalidades básicas que aceptan la solicitud y responden con un código adecuado, lo que permite la extensibilidad futura.
Por otro lado, el manejador GetActuatorCommandResourceHandler es un recurso observable que permite al GDA notificar al CDA mediante la especificación CoAP OBSERVE. Implementando la interfaz IActuatorDataListener, este manejador recibe actualizaciones de datos de actuadores desde DeviceDataManager a través del método onActuatorDataUpdate(). Este método actualiza los datos del actuador y notifica a los clientes conectados con la función super.changed(). Además, sobrescribe el método handleGET() para procesar solicitudes GET, donde se puede manejar el request y enviar una respuesta apropiada con el código de respuesta ResponseCode.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule08


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- 
- 
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- CoapClientToServerConnectorTest
- CoapServerGatewayTest
- 

EOF.
