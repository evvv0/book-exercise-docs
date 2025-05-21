# Constrained Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-CDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Mi implementación se centra en extender la clase MqttClientConnector del CDA para habilitar conexiones seguras mediante TLS y permitir la suscripción y el manejo de mensajes de comando de actuadores enviados desde el GDA. Además, actualicé las clases DeviceDataManager e IDataMessageListener para soportar la recepción y procesamiento de estos mensajes, permitiendo una comunicación bidireccional segura entre el GDA y el CDA. Esto incluye la configuración del cliente MQTT para usar certificados digitales, así como el diseño de métodos de callback específicos que interpretan los mensajes recibidos como objetos ActuatorData, que luego son procesados por el sistema local del CDA.

Asimismo, implementé la transmisión de datos desde el CDA hacia el GDA. Esto incluye el envío de SensorData y SystemPerformanceData a través de MQTT (o CoAP), y el análisis de los datos de sensores para detectar condiciones que activen eventos de actuación, como cambios en la temperatura más allá de los umbrales definidos.


How does your implementation work?

El funcionamiento de la implementación comienza habilitando la opción de cifrado, leyendo la configuración desde el archivo PiotConfig.props. Según esta configuración, se ajustan el puerto y los certificados necesarios para establecer una conexión segura. A continuación, se define un nuevo método dentro de la clase MqttClientConnector que permite establecer una referencia a un objeto IDataMessageListener. Cuando el cliente MQTT se conecta exitosamente al broker, se suscribe automáticamente al tema específico de comandos de actuadores. Al recibir un mensaje en ese tópico, el mensaje JSON se convierte en un objeto ActuatorData mediante la clase DataUtil. Este objeto es luego enviado al método handleActuatorCommandMessage() dentro de la clase DeviceDataManager, donde se procesa la acción correspondiente en el CDA.

Por otra parte, para la comunicación ascendente, se implementa el método _handleUpstreamTransmission() dentro de DeviceDataManager, que es responsable de enviar datos hacia el GDA utilizando MQTT o CoAP, dependiendo de la configuración o preferencia. Este método se invoca desde los manejadores de mensajes de sensor y de desempeño del sistema (handleSensorMessage() y handleSystemPerformanceMessage()), transmitiendo los datos en formato JSON a los recursos definidos para el GDA.

Finalmente, dentro del método _handleSensorDataAnalysis(), se realiza un análisis de los datos de temperatura recibidos. Si se detecta que la temperatura ha superado los límites inferiores o superiores configurados en PiotConfig.props, se genera automáticamente un evento de actuación para simular o emular un ajuste térmico.  


### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule10


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

- MqttClientPerformanceTest
- CoapClientPerformanceTest
- MqttClientConnectorTest
- DeviceDataManagerCallbackTest
- DeviceDataManagerIntegrationTest

# MQTT Client Performance Results
Se hizo una prueba para ver cuánto tarda el cliente MQTT en conectarse y desconectarse del broker, y el tiempo fue de unos 32.54 milisegundos. Después, se probaron tres niveles de calidad de servicio (QoS) enviando 10,000 mensajes de 264 bytes cada uno. Con QoS 0, que es el más rápido, tardó 0.677 segundos. Con QoS 1, el tiempo subió a 1.310 segundos, lo que es casi el doble (+93.5%). Finalmente, con QoS 2, que es el más confiable pero también el más lento, tardó 1.624 segundos, o sea, un 139.9% más que QoS 0. En resumen, cuanto mayor es el nivel de QoS, más tarda en enviar los mensajes.

# CDA CoAP Client Performance Test Results
Testing POST - CON POST message - useCON = True [10000]: 10207.891786 ms. Payload Len: 264

Testing POST - NON POST message - useCON = False [10000]: 8244.030923 ms. Payload Len: 264

El test con mensajes CON tardó aproximadamente 10.21 segundos, mientras que el test con NON fue más rápido, tomando unos 8.24 segundos. Eso significa que el uso de mensajes confirmables fue un 23.84% más lento que el de mensajes no confirmables. En resumen, NON fue más rápido y CON más lento, pero con más fiabilidad en la entrega.


EOF.
