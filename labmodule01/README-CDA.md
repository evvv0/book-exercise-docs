# Constrained Device Application (Connected Devices)

## Lab Module 01

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Mi implementación en Python consistió en configurar un entorno de desarrollo adecuado para ejecutar las pruebas unitarias y de integración de un proyecto IoT. Utilicé PyCharm como el entorno de desarrollo, donde me cree una cuenta. Luego configuré el PYTHONPATH y también modifiqué el archivo ConfigConst.py para establecer el valor de DEFAULT_CONFIG_FILE_NAME con la ruta absoluta de PiotConfig.props. Ejecuté las pruebas unitarias y de integración para verificar que la funcionalidad del sistema estuviera funcionando correctamente.

How does your implementation work? 
Mi implementación funciona configurando el entorno de desarrollo en PyCharm y asegurando que todas las dependencias necesarias estén disponibles a través de la correcta configuración de las rutas en PYTHONPATH que fue la siguiente:
$env:PYTHONPATH="C:\programmingtheiot\python-components\src\main\python;C:\programmingtheiot\python-components\src\test\python"
Toda esta configuración y pruebas fueron realizadas dentro de una nueva rama del repositorio llamada labmodule01.
### Code Repository and Branch

NOTE: Be sure to include the branch 

URL: https://github.com/evvv0/python-components/tree/labmodule01

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ConfigUtilTest
- 
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- ConstrainedDeviceAppTest
- 
- 

EOF.
