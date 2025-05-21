# Gateway Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Mi implementación actualiza la clase MqttClientConnector del Gateway Data Aggregator (GDA) para soportar conexiones MQTT con autenticación mediante usuario y contraseña, además de habilitar conexiones cifradas usando TLS. Esto permite que el GDA se conecte de manera segura al broker MQTT, mejorando la privacidad e integridad de los datos transmitidos. También se agregó la capacidad para cargar credenciales y certificados desde archivos de configuración externos, lo que facilita la gestión de seguridad sin necesidad de codificar información sensible dentro del código fuente.

Además, la implementación mejora la flexibilidad del cliente MQTT en el GDA al permitir configurar parámetros clave como el cliente ID, el puerto, el host, y opciones de reconexión automática. Esto hace que la conexión sea más robusta y configurable según el entorno donde se despliegue el sistema. En resumen, la implementación se enfoca en proporcionar una conexión segura, confiable y configurable entre el GDA y el broker MQTT para soportar las comunicaciones necesarias en el ecosistema IoT.

Paralelamente, se añadió funcionalidad al DeviceDataManager para manejar mensajes entrantes del CDA, específicamente SensorData, SystemPerformanceData y respuestas de ActuatorData. Para ello, se implementaron métodos especializados que reciben estos mensajes, los convierten de JSON a objetos Java y los procesan. En particular, se creó lógica para analizar datos de humedad en SensorData y generar eventos de actuación (actuador) cuando se detectan cruces de umbral configurados, como encender o apagar un humidificador, fomentando una respuesta automática basada en la información recibida.

How does your implementation work?

El funcionamiento inicia con la lectura de los parámetros de configuración desde el archivo PiotConfig.props, donde se extraen datos como el host del broker, puerto, cliente ID, y opciones relacionadas con la seguridad y la sesión MQTT. En caso de que se habilite la encriptación, se carga el certificado PEM especificado y se configura la conexión para usar TLS, asegurando que la comunicación con el broker sea cifrada.

Luego, si existe un archivo de credenciales configurado, la implementación lee el usuario y la contraseña para autenticar la conexión MQTT. Esto se realiza mediante un método dedicado que carga estos valores y los establece en las opciones de conexión. Posteriormente, el cliente MQTT se inicializa con los parámetros configurados, incluyendo la persistencia, el manejo de la sesión y la reconexión automática.

Al construir la URL de conexión, se concatena el protocolo (ya sea TCP o SSL) con el host y puerto definidos, y se prepara la conexión para establecerse con el broker. Esto garantiza que el cliente MQTT utilice los parámetros adecuados para su entorno y que soporte tanto conexiones seguras como no seguras, según lo definido en la configuración.

Para mejorar la estabilidad y evitar bloqueos al manejar mensajes simultáneos, el cliente MQTT se cambió a MqttAsyncClient, que funciona de forma asíncrona, permitiendo que el GDA reciba mensajes, los procese y envíe otros sin interrumpir el flujo.

Cuando la conexión con el broker se establece correctamente, el sistema se suscribe automáticamente a los temas MQTT del CDA que envían datos de sensores, rendimiento del sistema y respuestas de actuadores. Se crearon listeners que implementan IMqttMessageListener para recibir y convertir los mensajes JSON a objetos Java (SensorData, SystemPerformanceData, ActuatorData), y luego invocan métodos especializados en DeviceDataManager.

Dentro de DeviceDataManager, los mensajes de sensor son analizados para detectar cruces de umbral de humedad configurados en PiotConfig.props. Si se detectan niveles de humedad fuera de los límites definidos (por debajo del piso o por encima del techo), el sistema genera mensajes ActuatorData que ordenan activar o desactivar un humidificador. Para evitar reacciones erráticas, se implementa una lógica que requiere al menos dos cruces de umbral en un intervalo de tiempo configurable (por ejemplo, 5 minutos) para disparar la actuación.



### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule10



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

# GDA CoAP Client Performance Test Results
INFO: Testing PUT - CON May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest execTestPut INFO: PUT message - useCON = true [10000]: 18563218 ms May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest testPutRequestNon INFO: Testing PUT - NON May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest execTestPut INFO: PUT message - useCON = false [10000]: 242186 ms May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest testPostRequestCon INFO: Testing POST - CON May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest execTestPost INFO: POST message - useCON = true [10000]: 274792 ms May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest testPostRequestNon INFO: Testing POST - NON May 21, 2025 1:30:32 PM programmingtheiot.part03.integration.connection.CoapClientPerformanceTest execTestPost INFO: POST message - useCON = false [10000]: 724838 ms

Los tiempos registrados fueron: PUT-CON: 18,563,218 ms, PUT-NON: 242,186 ms, POST-CON: 274,792 ms y POST-NON: 724,838 ms. Al comparar los resultados tomando como referencia los modos NON, se observó que las solicitudes CON fueron significativamente más lentas, especialmente en PUT, con una diferencia del 98.7%. En contraste, POST-CON fue más rápido que POST-NON con una diferencia del 62.1%. En general, la prueba más rápida fue PUT-NON, mientras que la más lenta fue PUT-CON, lo que resalta el mayor coste en tiempo de los mensajes confirmables frente a los no confirmables.

EOF.
