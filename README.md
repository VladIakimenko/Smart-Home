## Project Description:

The project involves creating the backend for a web-based smart home interface. This backend is primarily an API that processes, stores, and serves data collected from various programmable sensors located around the smart home.

The sensors periodically record temperature measurements and photographs, and relay them to the API. The measurements involve the sensor's ID and the current temperature in Celsius. This data is processed by the API and stored for future retrieval or real-time use.

The API is implemented using Django REST Framework. It consists of two main models, several serializers, and viewsets that create the API endpoints.

### Models:
**Sensor:** Represents the programmable sensors in the system. Each sensor has a unique 'name' and a 'description' which can be left blank.  
**Reading:** Represents a measurement taken by a Sensor. It contains a foreign key to the associated sensor, the temperature reading, a timestamp ('created_at') of when the reading was taken, and an optional photograph.  

### Serializers:
**SensorSerializer:** Converts Sensor model instances into JSON and vice versa for creating and viewing sensor data.  
**ReadingSerializer:** Similar to SensorSerializer, but for the Reading model. It has a field 'sensor' that links the reading to a sensor using the sensor's primary key.  
**SensorDetailSerializer:** This serializer is used for retrieving a single sensor's details along with all its associated readings (measurements). The 'measurements' field uses the ReadingSerializer to represent each reading.  

### Views:
**SensorViewSet:** Provides list and create functionality for Sensor model instances.  
**SensorDetailViewSet:** Provides retrieve and update functionality for Sensor model instances, including their associated readings.  
**ReadingViewSet:** Provides create functionality for Reading model instances.  

### URLs:
**'/sensors/':** Allows listing and creating sensors.  
**'/sensors/<pk>/':** Allows retrieving and updating details of a particular sensor identified by its primary key.  
**'/measurements/':** Allows creating new measurements.  

## Functionality:
The following CRUD functionality is realized as follows:
- Create a new sensor by providing a name and optionally a description. This is done by a POST request to '/sensors/' endpoint.
- Update an existing sensor's details. This is done by a PUT or PATCH request to '/sensors/<pk>/' endpoint.
- Add a new temperature measurement from a specific sensor by providing the sensor ID and the temperature. This is done by a POST request to '/measurements/' endpoint.
- Retrieve a list of all sensors, with brief details (ID, name, and description) of each sensor. This is done by a GET request to '/sensors/' endpoint.
- Retrieve comprehensive details of a particular sensor, including its ID, name, description, and a list of all measurements (each with temperature and timestamp). This is done by a GET request to '/sensors/<pk>/' endpoint.
