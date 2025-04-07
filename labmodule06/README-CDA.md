# Constrained Device Application (Connected Devices)

## Lab Module 06

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Mi implementación permite la comunicación mediante MQTT en el proyecto CDA, gestionando la publicación y suscripción de mensajes entre el cliente y el broker. Inicialmente, creé un cliente MQTT que se conecta, publica mensajes y se suscribe a temas específicos. Luego, implementé los callbacks para manejar eventos como la conexión, desconexión y la recepción de mensajes. Después, añadí la capacidad de publicar mensajes a un tema (publishMessage), suscribirse a un tema (subscribeToTopic) y desuscribirse de un tema (unsubscribeFromTopic). Finalmente, integré el cliente MQTT dentro de la clase DeviceDataManager para automatizar el proceso de conexión al broker al iniciar el sistema y desconexión al detenerlo. Esto permite que el DeviceDataManager gestione la comunicación de manera fluida durante el ciclo de vida de la aplicación, con la posibilidad de subscribirse al recurso de comandos de actuadores y manejar la comunicación de manera eficiente.


How does your implementation work?
La implementación comienza con la creación de la clase MqttClientConnector, que configura el cliente MQTT con parámetros como el host, puerto, tiempo de keep-alive y clientID. A continuación, se gestionan las conexiones y desconexiones mediante métodos específicos. Los callbacks implementados gestionan eventos como la conexión (onConnect), desconexión (onDisconnect), la publicación de mensajes (onPublish), la recepción de mensajes (onMessage) y la suscripción a temas (onSubscribe). Posteriormente, agregué la funcionalidad para publicar y suscribirse a temas. Los métodos publishMessage y subscribeToTopic validan los parámetros, como el tema y el nivel de QoS, antes de realizar las acciones. En la última fase, integré el cliente MQTT en la clase DeviceDataManager. Dentro de su constructor, se verifica si MQTT está habilitado a través de la configuración, y si es así, se instancia el cliente MQTT y se configura para escuchar los mensajes de actuadores. En el método startManager(), se conecta al broker y se suscribe al tema de comandos de actuadores, mientras que en el método stopManager(), se desuscribe y desconecta. Esto asegura que la comunicación MQTT esté activada cuando el sistema está en funcionamiento y se apague correctamente cuando el sistema se detiene.




### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule06


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
