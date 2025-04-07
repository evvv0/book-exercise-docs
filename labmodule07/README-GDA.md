# Gateway Device Application (Connected Devices)

## Lab Module 07

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Esta implementación integra un cliente MQTT dentro del GDA, permitiendo la publicación de mensajes y la suscripción a temas mediante el protocolo MQTT. El cliente se conecta al broker MQTT y facilita la comunicación entre el GDA y el CDA, permitiendo que el GDA envíe comandos y reciba actualizaciones a través de suscripciones a temas específicos.

El MqttClientConnector actúa como una capa de abstracción, gestionando la conexión, publicación, suscripción y desconexión, además de manejar eventos clave como la conexión exitosa, pérdida de conexión y llegada de mensajes. Los logs permiten el seguimiento y la depuración en tiempo real del cliente MQTT. La integración de callbacks asegura que el cliente responda correctamente a estos eventos, y los logs permiten hacer un seguimiento y depuración en tiempo real del estado del cliente MQTT.

Se integra el cliente MQTT dentro del DeviceDataManager, habilitado por una variable booleana (enableMqttClient). Si está habilitado, se crea una instancia del cliente MQTT, que se conecta al broker y permite la interacción mediante publicaciones y suscripciones. También se gestionan adecuadamente la desconexión y desinscripción de temas cuando el DeviceDataManager se detiene, optimizando los recursos y la comunicación

How does your implementation work?
La implementación comienza con la creación de la clase MqttClientConnector, que interactúa con el broker MQTT usando la biblioteca Paho de Eclipse. Esta clase implementa dos interfaces clave: IPubSubClient para manejar la publicación y suscripción a mensajes, y MqttCallbackExtended para gestionar respuestas del broker, como la conexión y la llegada de mensajes. Los parámetros del cliente MQTT, como host, puerto y el intervalo de keep alive, se configuran desde un archivo de configuración.

Se implementan métodos como connectClient() y disconnectClient() para gestionar la conexión y desconexión del broker, garantizando que el cliente se conecte y desconecte adecuadamente. Los callbacks connectComplete(), connectionLost() y messageArrived() se implementan para manejar eventos como la conexión exitosa, la pérdida de conexión y la llegada de mensajes.Otros métodos son:

publishMessage(): Publica un mensaje en un tema específico, validando tanto el nombre del tema como el nivel de QoS. Si el QoS es válido, se publica el mensaje; si no, se maneja el error y se devuelve false.

subscribeToTopic(): Permite suscribirse a un tema determinado, validando también el nombre del tema y el QoS. Si la suscripción es exitosa, devuelve true; de lo contrario, se maneja el error y devuelve false.

unsubscribeFromTopic(): Desuscribe del tema especificado. Similar a los otros métodos, valida el nombre del tema y devuelve true si la desuscripción es exitosa.

isConnected(): Verifica si el cliente está conectado al broker, basado en el estado actual de la conexión.

El DeviceDataManager integra el cliente MQTT mediante la variable booleana enableMqttClient. Si se habilita, se crea una instancia del cliente MQTT. En el método initManager(), se crea esta instancia y se asocia a la variable mqttClient, habilitando la recepción de mensajes.

En el método startManager(), se establece la conexión con el broker mediante mqttClient.connectClient(). Si la conexión es exitosa, se suscribe a los temas relevantes del GDA y los datos de sensores o actuadores. Si la conexión falla, se registran los errores para tomar las acciones necesarias. Finalmente, en stopManager(), se asegura la desconexión adecuada, cancelando suscripciones y cerrando la conexión.



### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule07


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
- MqttClientControlPacketTest
- 

EOF.
