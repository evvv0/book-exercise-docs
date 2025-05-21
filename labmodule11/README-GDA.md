# Gateway Device Application (Connected Devices)

## Lab Module 11

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Mi implementación mejora el conector MQTT (MqttClientConnector) para cargar configuraciones flexibles desde diferentes secciones del archivo PiotConfig.props, permitiendo usar perfiles estándar o específicos para un gateway en la nube. Se añaden métodos protegidos para publicar y suscribirse a tópicos MQTT.

Cuando se establece la conexión MQTT, el método connectComplete() configura automáticamente suscripciones a tópicos relevantes, utilizando callbacks para procesar los mensajes entrantes. Esto permite una respuesta dinámica a datos de sensores, actuadores y rendimiento, tanto en entornos locales como en la nube.

Para gestionar la comunicación con el gateway en la nube, desarrollé la interfaz ICloudClient y su implementación CloudClientConnector, que delega gran parte de las operaciones al conector MQTT. Esta clase maneja la conexión, la publicación y la suscripción a tópicos en la nube, así como el intercambio de datos relevantes del sistema. Además, se integra con DeviceDataManager para habilitar o deshabilitar la conexión con la nube según la configuración.

En conjunto, el sistema conecta al CDA, GDA y un servicio en la nube para la recolección, almacenamiento y análisis de datos. Los datos de sensores y los de rendimiento del sistema son enviados al servicio en la nube a través del GDA.

Cuando la nube detecta que un valor (en este caso la temperatura) supera un umbral configurado, se publica un evento para encender o apagar un LED. El GDA, suscrito a ese tópico, recibe el comando, lo convierte en una orden para el CDA, y este activa el LED. El resultado puede verificarse mediante registros o emulación física.


How does your implementation work?
Mi implementación amplía la funcionalidad original del MqttClientConnector permitiendo cargar configuraciones desde diferentes secciones del archivo de propiedades. Esto habilita un constructor que selecciona entre la configuración por defecto o la específica para el gateway en la nube. Cuando se establece la conexión MQTT, el método connectComplete() verifica si se está usando la configuración del gateway en la nube. En ese caso, se suscribe a los tópicos relevantes mediante un listener anidado que recibe y procesa los mensajes MQTT, llamando a los métodos adecuados según el tipo de mensaje (sensores, actuadores, etc.).

Los métodos para publicar y suscribirse (publishMessage(), subscribeToTopic(), unsubscribeFromTopic()) encapsulan la lógica para interactuar con el broker MQTT, haciendo validaciones básicas antes de actuar. Esto permite que otras clases dentro del paquete o subclases los usen o extiendan sin exponerlos públicamente. Además, se incluye un mecanismo para asignar un IConnectionListener que notifica cuando la conexión MQTT se establece o se pierde.

La clase CloudClientConnector inicializa un prefijo de tópico para la nube, asegurándose de que tenga el formato correcto. Implementa la interfaz ICloudClient y usa internamente una instancia de MqttClientConnector para manejar la conexión real con el broker. Al llamar a connectClient(), se crea y conecta el cliente MQTT con la configuración del gateway en la nube. Para publicar datos, se convierten objetos como SensorData o SystemPerformanceData a JSON y se envían a tópicos formados dinámicamente, aplicando el nivel de calidad de servicio configurado. El conector se suscribe a tópicos específicos en la nube y procesa los mensajes recibidos, además de incluir métodos para desuscribirse, desconectar y gestionar la comunicación con listeners y otros componentes.

CloudClientConnector se integra con DeviceDataManager, que decide mediante una bandera si se habilita la conexión con la nube y controla el ciclo de vida del cliente, además de delegar el manejo de mensajes de sensores, actuadores y rendimiento. El flujo general comienza con la recolección de datos en el CDA, que los envía al GDA. Luego, el GDA transmite estos datos al servicio en la nube mediante tópicos MQTT configurados para cada tipo de dato.El servicio en la nube almacena y monitorea estos datos, y si detecta que alguno supera un umbral, publica un evento para controlar un LED (encender o apagar). El GDA, a través de CloudClientConnector, está suscrito a ese tópico de eventos. Al recibir un mensaje, convierte el JSON en un objeto ActuatorData y traduce el comando (por ejemplo, 0 para encender o 1 para apagar el LED), que luego envía al CDA mediante MQTT o CoAP. En este caso el evento consite en si se supera un umbral de temperatura. Finalmente, el CDA interpreta el comando y cambia el estado del LED.


### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule11


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

- MqttClientConnectorTest
- CloudClientConnectorTest
- 

EOF.
