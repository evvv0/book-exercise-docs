# Gateway Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-GDA-* issues.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

La implementación consiste en integrar y gestionar módulos dentro de la aplicación GDA para recolectar datos de rendimiento del sistema, como la utilización de la CPU y la memoria. Los módulos permiten monitorear de forma eficiente los recursos del sistema. El SystemPerformanceManager es el responsable de iniciar y detener las tareas de monitoreo, mientras que las clases SystemCpuUtilTask y SystemMemUtilTask se encargan de obtener los datos específicos sobre el uso de la CPU y la memoria, respectivamente.

How does your implementation work?

El sistema se compone de varias clases interconectadas que trabajan de forma modular. SystemPerformanceManager coordina el inicio y la detención de las tareas, mientras que las clases SystemCpuUtilTask y SystemMemUtilTask ejecutan las funciones específicas de monitoreo. Estas tareas heredan de la clase base BaseSystemUtilTask, que contiene la funcionalidad común para todas las tareas de rendimiento. La implementación también incluye un conjunto completo de pruebas unitarias para asegurar que no se introduzcan errores en el sistema, y pruebas de integración que validan la correcta interacción entre los módulos.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/java-components/tree/labmodule02


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ConfigUtilTest
- SystemCpuUtilTaskTest
- SystemMemUtilTaskTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SystemPerformanceManagerTest
- GatewayDeviceAppTest
- 

EOF.
