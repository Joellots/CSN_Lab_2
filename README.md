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
  - Below is a mapping of the components that make up the system (within the context of a layered architecture). See Picture 1. 
    
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
