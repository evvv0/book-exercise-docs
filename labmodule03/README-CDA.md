# Constrained Device Application (Connected Devices)

## Lab Module 03

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Mi implementación tiene como objetivo la simulación de datos de sensores y actuadores para probar sistemas sin necesidad de tener hardware físico. El enfoque principal es la gestión de sensores, actuadores y el rendimiento del sistema. Para lograrlo, se utiliza un generador de datos que simula valores de sensores como temperatura, humedad y presión y simula la interacción con actuadores como humidificadores o sistemas HVAC. Utilizando clases como SensorData y ActuatorData, se gestionan los datos generados por los sensores y los estados de los actuadores. Además, implementé clases como SensorAdapterManager y ActuatorAdapterManager, que manejan la lógica de adaptación entre los sensores y actuadores simulados y otros módulos del sistema. El DeviceDataManager se encarga de coordinar y centralizar los datos generados por estos dispositivos, asegurando que se gestionen de forma eficiente y coherente a través del sistema.

How does your implementation work?

La implementación trabaja mediante una serie de clases y tareas que generan y gestionan los datos de los sensores y actuadores. Modifique las clases base como BaseSensorSimTask y BaseActuatorSimTask, que luego son extendidas para cada tipo específico de sensor, como HumiditySensorSimTask o TemperatureSensorSimTask, y actuador, como HumidifierActuatorSimTask. Cada tarea simula la generación de datos en intervalos regulares, y estos datos se encapsulan en objetos como SensorData o ActuatorData. El SensorAdapterManager y ActuatorAdapterManager son responsables de manejar la comunicación entre los sensores/actuadores simulados y el resto de la aplicación. Cada tipo de sensor y actuador tiene su clase específica (como HumiditySensorSimTask o HvacActuatorSimTask) que genera los datos correspondientes. Estos datos son luego gestionados y coordinados por el DeviceDataManager, que asegura que la información fluya correctamente entre los dispositivos y los módulos del sistema.

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule03

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ActuatorDataTest
- SensorDataTest
- SystemPerformanceDataTest
- HumiditySensorSimTaskTest
- PressureSensorSimTaskTest
- TemperatureSensorSimTaskTest
- HumidifierActuatorSimTaskTest
- HvacActuatorSimTaskTest
- BaseIotData

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SensorAdapterManagerTest
- ActuatorAdapterManagerTest
- DeviceDataManagerNoCommsTest
- ConstrainedDeviceAppTest

EOF.
