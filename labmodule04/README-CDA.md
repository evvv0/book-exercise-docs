# Constrained Device Application (Connected Devices)

## Lab Module 04

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
La implementación se centra en la integración de sensores y actuadores emulados dentro de la aplicación ConstrainedDeviceApp (CDA). Esta integración permite simular dispositivos como el humidificador, el sistema HVAC y la pantalla LED sin necesidad de hardware físico. Para ello, se utilizaron bibliotecas como Pisense y Sense-Emu para crear tareas que emulan sensores de temperatura, humedad y presión, y actuadores que simulan la interacción con estos dispositivos. Utilizando clases como SensorAdapterManager y ActuatorAdapterManager, la implementación gestiona la carga dinámica de los dispositivos emulados según la configuración del sistema. Esta estructura facilita pruebas más ágiles y eficientes en entornos controlados.

How does your implementation work?
La implementación comienza con la instalación de las bibliotecas necesarias (Pisense y Sense-Emu) dentro de un entorno WSL (Windows Subsystem for Linux). Todas las pruebas se ejecutan desde la consola de WSL. Lo siguiente que realice fue establecer el parámetro enableEmulator a True en PiotConfig.props. 

Los sensores emulados, como TemperatureSensorEmulatorTask, HumiditySensorEmulatorTask y PressureSensorEmulatorTask, son cargados dinámicamente mediante import_module(), lo que garantiza que solo se carguen si el emulador está habilitado. Del mismo modo, en la clase ActuatorAdapterManager, se gestionan los actuadores emulados como HumidifierEmulatorTask y HvacEmulatorTask.

A continuación, se modificó la clase SensorAdapterManager para integrar estos sensores emulados. Esta clase se encarga de gestionar la comunicación entre los sensores emulados y el resto del sistema. Luego, la clase ActuatorAdapterManager se encargó de gestionar la interacción con los actuadores emulados, permitiendo la activación y desactivación de estos actuadores en función de las tareas asignadas, todo dentro del entorno controlado del emulador. Esta estructura modular y flexible facilita las pruebas y simulaciones sin necesidad de un dispositivo físico real.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule04


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

- SenseHatEmulatorQuickTest.py
- HumidityEmulatorTaskTest.py
- PressureEmulatorTaskTest.py
- TemperatureEmulatorTaskTest.py
- HumidifierEmulatorTaskTest.py
- HvacEmulatorTaskTest.py
- LedDisplayEmulatorTaskTest.py
- SensorEmulatorManagerTest.py
- ActuatorEmulatorManagerTest.py

EOF.
