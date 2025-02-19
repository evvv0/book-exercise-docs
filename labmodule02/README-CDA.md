# Constrained Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Lo que hice en esta implementación fue agregar la funcionalidad de monitoreo de rendimiento del sistema dentro de la aplicación ConstrainedDeviceApp (CDA). Básicamente, ahora la app puede recolectar datos sobre el uso del CPU y la memoria, para que se puedan analizar y tomar decisiones basadas en ellos.

How does your implementation work?

Para lograr esto, edité el módulo llamado SystemPerformanceManager, que es el encargado de manejar las tareas de monitoreo. Estas tareas están organizadas de manera modular, con una clase base (BaseSystemUtilTask) de la cual heredan SystemCpuUtilTask (para monitorear el CPU) y SystemMemUtilTask (para monitorear la memoria). Todo esto se conecta a la aplicación principal, permitiendo iniciar y detener el monitoreo cuando sea necesario. 

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule02

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
- ConstrainedDeviceAppTest
- 
  

EOF.
