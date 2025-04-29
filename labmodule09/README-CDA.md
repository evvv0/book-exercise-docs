# Constrained Device Application (Connected Devices)

## Lab Module 09

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Mi implementación permite que un cliente CoAP se comunique de manera efectiva con un servidor CoAP dentro de un entorno de Internet de las Cosas (IoT), facilitando el intercambio de datos estructurados como métricas de sensores y comandos de actuadores. Esta funcionalidad incluye la capacidad de enviar solicitudes GET, tanto confirmables como no confirmables, así como también realizar solicitudes de descubrimiento de recursos disponibles en el servidor. A través de esta implementación, el cliente puede emitir peticiones hacia rutas específicas del servidor y procesar las respuestas recibidas para su posterior uso en la aplicación. Esto permite integrar dispositivos IoT que necesiten obtener información actualizada o identificar qué servicios ofrece un servidor en un momento dado.

How does your implementation work?
La lógica se basa en el uso de la biblioteca aiocoap, que permite el manejo asincrónico del protocolo CoAP. La clase define un método que construye la ruta del recurso solicitado a partir de parámetros dados, y luego inicia una solicitud GET utilizando una corrutina que se ejecuta en el bucle de eventos de Python. Esta solicitud es enviada al servidor como un mensaje CoAP, el cual puede ser de tipo confirmable (CON) o no confirmable (NON) dependiendo de la configuración. Una vez enviada, la implementación espera la respuesta del servidor y, al recibirla, procesa su contenido. Si el recurso recibido corresponde a un comando de actuador, se decodifica y se transforma en un objeto específico que luego se entrega a un componente encargado de manejar ese tipo de datos. En el caso de otras respuestas, se registran e interpretan de forma genérica. Además, se implementó una función para realizar una solicitud GET especial hacia la ruta .well-known/core, lo que permite obtener una lista de los recursos disponibles en el servidor. Todo el flujo de comunicación se apoya en el registro de eventos mediante logs para facilitar el seguimiento y la depuración del sistema.


### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule09



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

- CoapClientConnectorTest
- 
- 

EOF.
