# Constrained Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
Mi implementación en el Lab Module 05 se centra en dos cosas importantes: recoger y gestionar los datos de rendimiento del sistema (como el uso de la CPU y la memoria), y convertir ciertos objetos a formato JSON y viceversa. Para la primera parte, actualicé la clase SystemPerformanceManager para que recoja datos sobre la utilización de la CPU y la memoria, los guarde en un objeto SystemPerformanceData, y si hay un "listener" configurado (una especie de receptor de los datos), lo avisa para que reciba esos datos. En la segunda parte, trabajé en la clase DataUtil para convertir objetos como ActuatorData, SensorData y SystemPerformanceData a JSON y también para convertirlos de nuevo a objetos a partir de JSON.

How does your implementation work?
La implementación funciona en dos pasos. Primero, en la clase SystemPerformanceManager, modifiqué el método handleTelemetry() para que recoja el uso de la CPU y la memoria y los almacene en un objeto SystemPerformanceData. Si hay un listener configurado, este recibirá esos datos para que los procese. 

En segundo lugar, la implementación de la clase DataUtil se enfoca en facilitar la conversión entre objetos específicos (como ActuatorData, SensorData y SystemPerformanceData) y su representación en formato JSON, lo cual es fundamental para la serialización y deserialización de los datos en la aplicación.

Para convertir los objetos en JSON, se utilizan los métodos actuatorDataToJson, sensorDataToJson y systemPerformanceDataToJson. Estos métodos toman las instancias de las clases correspondientes y las convierten a una cadena en formato JSON utilizando json.dumps. La clase JsonDataEncoder es clave en este proceso, ya que garantiza que los atributos del objeto se conviertan correctamente en el formato JSON. Además, si el parámetro encodeToUtf8 está activado, la conversión se realiza en formato UTF-8, lo que asegura la compatibilidad con sistemas que requieran este tipo de codificación.

Por otro lado, los métodos jsonToActuatorData, jsonToSensorData y jsonToSystemPerformanceData realizan el proceso inverso, es decir, convierten las cadenas JSON de vuelta en objetos de las clases correspondientes. Para esto, se utiliza un método auxiliar, _jsonToObject, que primero formatea el JSON (cambiando las comillas simples por dobles y ajustando los valores booleanos) y luego lo carga en un diccionario. A continuación, se asignan los valores del diccionario a los atributos del objeto, asegurando que el objeto restaurado sea una representación fiel del original.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/evvv0/python-components/tree/labmodule05


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- DataUtilTest
- 
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SystemPerformanceManagerTest
- DataIntegrationTest
- 
  

EOF.
