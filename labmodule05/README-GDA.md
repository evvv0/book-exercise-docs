# Gateway Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-GDA-* issues (requirements) listed.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

La implementación gestiona diferentes tipos de datos dentro de un sistema IoT, como información de sensores, actuadores, rendimiento del sistema y estado general. Las clases como ActuatorData, SensorData, SystemPerformanceData y SystemStateData están basadas en una estructura común (BaseIotData), lo que facilita su interacción. Además, se actualiza SystemPerformanceManager para almacenar datos de rendimiento como CPU, memoria y disco. DataUtil convierte estas clases a JSON y viceversa. DeviceDataManager se encarga de la inicialización, inicio y detención de servicios clave en el dispositivo, como la gestión del rendimiento del sistema y servicios de conexión. Finalmente, se integra DeviceDataManager en la aplicación principal GatewayDeviceApp.

How does your implementation work?

La implementación está organizada para manejar de manera eficiente los datos de un sistema IoT. Primero, se definen varias clases que representan los diferentes tipos de datos del sistema, todas ellas heredando de una clase base común llamada BaseIotData. Esta estructura permite que los objetos de estas clases sean tratados de manera uniforme, lo que facilita su manejo y manipulación dentro del sistema. Para permitir la comunicación entre el CDA y el GDA, se implementan métodos en la clase DataUtil que convierten estas clases a formato JSON y viceversa, utilizando la biblioteca Gson. Esto facilita la transmisión de los datos entre el dispositivo IoT y otros componentes, como servidores en la nube, de manera sencilla y estándar. 

En cuanto al rendimiento del sistema, la implementación cuenta con SystemPerformanceManager que se se actualiza periódicamente y es controlado desde la clase DeviceDataManager, que es la responsable de manejar la inicialización y gestión de servicios clave en el dispositivo IoT.

DeviceDataManager es el encargado de gestionar los servicios de conexión y de rendimiento del sistema. Dependiendo de la configuración, esta clase instanciará y gestionará diferentes servicios, como MQTT o CoAP para la comunicación, o clientes para la nube, asegurándose de que se habiliten o deshabiliten de acuerdo con las necesidades del sistema. Por último, este se integra dentro de la aplicación principal GatewayDeviceApp. Esta clase principal se encarga de controlar el ciclo de vida de la aplicación, invocando los métodos startManager() y stopManager() para iniciar y detener los servicios según sea necesario, asegurando que los diferentes componentes del sistema IoT estén siempre operativos o se detengan adecuadamente cuando sea necesario.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule05


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ActuatorDataTest
- SensorDataTest
- SystemPerformanceDataTest
- SystemStateDataTest
- DataUtilTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SystemPerformanceManagerTest
- DataIntegrationTest
- DeviceDataManagerNoCommsTest
- GatewayDeviceAppTest

EOF.
