# CSN_Lab_2
## PART B [Team Work]
### Done by:
### Etienne Fuh, Aram Burlakov, Julio, Okore Joel

## Task 3:
3.1.
  - Functional Requirements:
      1. Real-Time Data Collection: Devices will continuously send their status and telemetry data to the backend. This data must be collected efficiently, with minimal latency, to reflect almost real-time information on the dashboard.
      2. Pre-defined Queries: Handles all pre-defined queries from the customers. Interfaces directly with the Time-Series Database and NoSQL Database to fetch the required data. The service can optimize and cache query results to improve performance.
      3. Dashboard Presentation: A web-based dashboard will serve the end-users, providing an aggregated view of all the connected devices' status, along with pre-defined queries for deeper insights.
      4. Data Storage: Since the data is stateless and primarily read-only, a database optimized for fast read operations will be used. Depending on the use cases, a time-series database would be appropriate to store status data points over time.

  - Non-Functional Requirements:
      1. Security and Access Control: Given the nature of IoT devices and sensitive data, security will be of great importance. This includes secure data transmission, authentication, authorization, and auditing.
      2. Efficiency: The incoming data will be ingested into the system through a robust data pipeline that can handle multiple data sources concurrently. This pipeline will parse, clean, and prepare the data for presentation on the dashboard.
      3. Scalability and Performance: The use of caching, stream processing, and efficient databases ensures that the system remains performant and scalable as the number of IoT devices and users grows.
      4. Compatibility: The use of intermediary connectors like relay and ESP-32 will ensure that the system can be integrated seamlessly into different IoT infrastructure, irrespective of the vendors or manufacturers.
      5. Reliability: Implementing component redundancy and logging/monitoring, both in local and cloud infrastructure, enhance fault tolerance and failure detection.
      6. Maintainability: Modularity of subsystems within the choosen layered architecture ensure that each module can be individually analyzed, modified and tested without affect entire system operations
   
3.2. Component Mapping
  - Below is a mapping of the components that make up the system (within the context of a layered architecture). See picture 1. 
    
![Is3_Architecture_main](https://github.com/user-attachments/assets/e90e5c35-a937-4478-b685-439dd14e7128)
Picture 1 - Component Mapping

3.3. Technology Stack
  - IoT Device Communication: MQTT (EMQX or Mosquitto), HTTP(S), WebSocket
  - Data Ingestion: Apache Kafka
  - Data Processing: Apache NiFi
  - Stream Processing: Apache Flink
  - Queries Engine: Elasticsearch
  - Time-Series Database: InfluxDB
  - NoSQL Database: MongoDB
  - Backend API: Node.js
  - Frontend: React.js
  - Authentication & Security: OAuth 2.0, JWT, Keycloak
  - Monitoring & Logging: Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana), Alertmanager

## Architecture Documentation
### Architectural goals
  The architecture is designed for real-world applications catering to users who require centralized management of IoT devices, by providing a integrated platform for monitoring diverse IoT devices. Every IoT device, including cameras, electric switches, refrigerators, thermostats, intercoms, and more, has a corresponding app that can be used to control it from a smartphone. The primary objective is to have a unified view of all devices on one display. The architecture needs to provide for a dashboard system that can inform on the state of its clients' devices nearly instantly. The program collects stateless data from registered Internet of Things devices and turns it into an aesthetically pleasing dashboard that shows the customer's devices' activities. 

### Decision and Justification of Technogy Stack

#### Data Collection Layer: EMQX (MQTT Broker), AWS API Gateway, Apache Kafka, Apache NiFi
This layer is responsible for collecting data from IoT devices. It handles different communication protocols like MQTT and HTTP to gather data reliably from various sensors and actuators.
  - EMQX: Used as an MQTT broker to manage lightweight messaging between IoT devices
  - AWS API Gateway: Allows REST-based communication for devices that do not use MQTT.
  - Apache Kafka: A event streaming platform to handle large volumes of real-time data from IoT devices.
  - Apache NiFi: Provides powerful data routing and transformation, allowing efficient data flow between devices and the cloud.

#### Data Management Layer: Apache Flink, Elasticsearch, InfluxDB, MongoDB, AWS S3
This layer processes and stores the collected data. It handles both real-time and historical data storage requirements.
  - Apache Flink: Suitable for stream processing to analyze real-time data.
  - Elasticsearch: Provides fast search and analytics capabilities, making it ideal for indexing device logs and finding patterns.
  - InfluxDB: Designed for time-series data, perfect for sensor data like temperature, humidity, and energy consumption.
  - MongoDB: Flexible schema makes it a good choice for storing metadata about IoT devices configurations and user data.
  - AWS S3: AWS S3 plays a crucial role in video transmission by serving as a scalable and durable storage solution.

When video data is captured from IoT devices, it can be uploaded to S3, where it is stored securely and efficiently. S3 supports high-throughput data handling, making it ideal for video streaming. With its integration with AWS services, video data stored in S3 can be easily accessed, processed, or streamed to other applications, ensuring reliable and low-latency delivery to end-users.

#### Monitoring and Logging: Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana), Alertmanager
This layer focuses on ensuring the system's health and reliability by monitoring key metrics, logging, and providing alerts when anomalies are detected.
  - Prometheus: Provides real-time monitoring and alerting based on predefined conditions.
  - Grafana: Works with Prometheus to visualize real-time data and long-term trends, helping operators to easily identify issues.
  - ELK Stack: Collects and stores logs from all system components, with Logstash for ingesting logs, Elasticsearch for indexing logs, and Kibana for log analysis.
  - Alertmanager: Automatically sends notifications based on alert rules, helping admins react quickly to potential problems.

#### Backend and APIs: Node.js, GraphQL, WebSocket, OAuth 2.0, JWT (JSON Web Tokens),	Keycloak
The backend layer is where application logic resides. This layer facilitates interaction between the front-end (Dashboard) and the data processing/storage systems. It also provides security mechanisms for user authentication and authorization.
  - Node.js: A lightweight, fast runtime environment for building scalable network applications that can manage numerous IoT devices simultaneously.
  - GraphQL: Used to optimize querying by making use of APIs.
  - WebSocket: Enables real-time, two-way communication between the server and clients, between the backend and dashboard
  - OAuth 2.0: An industry-standard protocol for authorization.
  - JWT (JSON Web Tokens): Ensures secure user sessions by embedding user roles and authentication information in encrypted tokens.
  - Keycloak: Manages identity and access control, providing a centralized solution for handling OAuth 2.0 and JWT authentication.

#### Dashboard and Front-End Layer: React
The front-end dashboard, developed with React, provides a graphical user interface for monitoring IoT devices. Real-time data from the back-end is displayed for users to analyze and act upon.

  - Below is the architectural component mapping, with a focus on the technology stack. See picture 2.
    
![image](https://github.com/user-attachments/assets/2edf021c-c725-46be-866a-bd53fdd33622)
Picture 2 - Component Mapping (Technology Stack View)

### Architectural Description
#### Class Diagram
The class diagram describes the relationships and interactions between the core components of the IoT system. See picture 3.

![Class_Diagram](https://github.com/user-attachments/assets/3d289e59-0d65-47c8-bbb6-0ea39bb45176)
Picture 3 - Class Diagram

#### Process Model
The process model focuses on the high-level structure of the application, showing how components interact in real time. See picture 4.

![Process_Diagram](https://github.com/user-attachments/assets/c7131e2f-c013-46c9-89bd-13b541727379)
Picture 4 - Process model

#### Development Model (Package Diagram)
The package diagram represents how the system is organized into different modules, focusing on separation of concerns and modularity. See picture 5. 

![Package_Diagram](https://github.com/user-attachments/assets/51c54ad5-3321-4cdd-bb6f-de53cf7c8b3f)
Picture 5 - Package Diagram

#### Deployment Diagram 
The deployment diagram focuses on how the software components of the system are deployed on the physical hardware and the communication links between them. See picture 6.

![Deployment_Diagram](https://github.com/user-attachments/assets/908e816e-ab93-45e5-91d2-eb9178540824)
Picture 6 - Deployment Diagram









  
