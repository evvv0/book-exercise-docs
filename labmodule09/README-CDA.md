# Constrained Device Application (Connected Devices)

## Lab Module 09

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Mi implementación consiste en un cliente CoAP llamado CoapClientConnector, que utiliza la librería aiocoap para facilitar la comunicación con servidores CoAP. Este cliente soporta solicitudes GET, POST, PUT, DELETE y OBSERVE, permitiendo la interacción con sensores y actuadores. La clase implementa la interfaz IRequestResponseClient y se integra con el módulo DeviceDataManager, permitiendo enviar y recibir datos de forma eficiente.

El cliente soporta solicitudes GET tanto confirmables como no confirmables, gestionando respuestas en formato JSON y convirtiéndolas en objetos de tipo ActuatorData. También incluye descubrimiento de recursos a través de solicitudes GET al path .well-known/core. Además, se implementa soporte para solicitudes PUT y POST, permitiendo modificar recursos y enviar datos al servidor. También cuenta con soporte para solicitudes DELETE, lo que permite eliminar recursos remotos.

Una característica clave de la implementación es el soporte para solicitudes OBSERVE, que permite al cliente suscribirse a un recurso y recibir actualizaciones automáticas cuando el recurso cambia, sin necesidad de solicitudes repetidas. Los métodos startObserver() y stopObserver() permiten gestionar la observación de recursos.


How does your implementation work?

Mi implementación funciona creando un cliente CoAP asíncrono utilizando la biblioteca aiocoap. La clase CoapClientConnector se inicializa cargando los parámetros de configuración (como host y puerto) desde un archivo, luego crea un cliente CoAP con un contexto asíncrono manejado por asyncio. Para interactuar con los recursos del servidor, la clase implementa los métodos de la interfaz IRequestResponseClient, lo que permite enviar solicitudes como GET, PUT, POST y DELETE.

Cada tipo de solicitud se maneja a través de métodos específicos que construyen y envían los mensajes CoAP, esperando las respuestas de manera asíncrona. Al recibir las respuestas, se procesan a través de métodos de callback para validar y registrar los datos. Además, se ha implementado una funcionalidad de descubrimiento de recursos que permite al cliente identificar dinámicamente los recursos disponibles en el servidor CoAP mediante una solicitud GET al path especial .well-known/core.

Además, se incorporaron métodos para observar recursos de manera continua utilizando los métodos startObserver() y stopObserver(), lo que permite al cliente suscribirse a un recurso y recibir actualizaciones automáticas cada vez que el recurso cambia. Esta observación se maneja de forma asíncrona, utilizando un rastreador interno para mapear los recursos observados y sus manejadores de respuesta.




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
