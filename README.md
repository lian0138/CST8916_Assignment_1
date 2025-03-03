## Introduction
The health monitoring application "POT" (平安通) represents a collaborative initiative between the Macau government and CTM (Companhia de Telecomunicações de Macau), where I was part of the development team at CTM. This project aims to enhance the health and safety of the elderly population in Macau by utilizing wearable technology to monitor health conditions in real time. My role in the project involved working closely with the technology stack, specifically focusing on implementing WebSockets for immediate data transmission. Insights gained from this experience will inform the analysis and recommendations detailed in this report.

## Section 1: REST and GraphQL for Data Requests and Updates
### REST for Data Requests and Updates
In the health monitoring application POT (平安通), a partnership project with the Macau government and developed through my previous company, CTM, we can structure a REST API to manage data requests and updates effectively. The endpoints might include:

GET /users/{id} : Retrieves user information such as health metrics and monitoring history for older citizens enrolled in the program.
POST /users: Creates entries for new users (elderly participants) who start using the health monitor.
PUT /users/{id} : Updates an existing user's health information based on insights or changes detected by the wearable device.
DELETE /users/{id} : Removes a user from the system, for instance, if they have ceased using the device or passed away.

For the POT application, even we didn't use GraphQL to build up the APIs, but it can be a powerful alternative to fetch specific health data. A GraphQL query could look something like this:
```
{
  user(id: "1") {
    id
    name
    healthMetrics {
      heartRate
      bloodPressure
      oxygenSaturation
    }
  }
}
```

An update operation could be performed as follows:
```
mutation {
  updateUserHealthMetrics(id: "1", metrics: { heartRate: 72, bloodPressure: { systolic: 130, diastolic: 85 }, oxygenSaturation: 95 }) {
    success
    message
  }
}
```

### Comparison of REST versus GraphQL for the Health Monitoring Application "POT"

| Feature                | REST                                      | GraphQL                                   |
|------------------------|-------------------------------------------|-------------------------------------------|
| **Data Retrieval**     | Simple and straightforward; can lead to over-fetching. | Clients request exact data needed, reducing payload. |
| **Endpoint Structure** | Clear endpoints for CRUD; requires multiple for different resources. | Single endpoint for various queries; initial setup is complex. |
| **Efficiency**         | Benefits from HTTP caching; separate requests may create bottlenecks. | Aggregates data efficiently; requires optimization. |
| **Real-time Capabilities** | Supports polling for updates; not primarily designed for real-time. | Supports real-time subscriptions but adds complexity. |
| **Learning Curve**     | Easier for those familiar with HTTP; can become complex with relationships. | Streamlined interaction but has a steeper learning curve. |

### Conclusion

In the **POT** (平安通) application, **REST** APIs effectively manage user data with a clear and maintainable structure. While GraphQL offers greater flexibility, its complexity may not be necessary for the project’s needs. The combination of REST for data management and WebSockets for real-time updates supports effective health monitoring for elderly citizens.

## Section 2: WebSockets for Real-time Communication

In the **POT** (平安通) health monitoring application, WebSockets enable seamless real-time communication between wearable devices and the server. 

### How WebSockets are Used in POT

1. **Persistent Connection**: Wearable devices establish a continuous WebSocket connection to the server, allowing ongoing data exchange.

2. **Immediate Data Sharing**: Vital health metrics (e.g., heart rate) are sent to the server at regular intervals, ensuring users' health data is always up-to-date.

3. **Real-time Alerts**: The server can push alerts directly to devices upon detecting abnormal health metrics (e.g., irregular heart rate), enabling quick responses.

4. **Bidirectional Communication**: WebSockets allow two-way communication, so the server can send updates instantly, enhancing user engagement and safety.

#### WebSockets vs. REST and GraphQL

| Feature                    | WebSockets                  | REST                  | GraphQL               |
|----------------------------|-----------------------------|-----------------------|-----------------------|
| **Connection Type**        | Persistent, full-duplex.    | Stateless requests.    | Stateless requests.    |
| **Data Flow**              | Real-time, bidirectional.   | Request-driven.        | Typically request-driven, with subscriptions. |
| **Efficiency**             | Instant updates, low latency. | Can experience delays. | Flexible, but may require multiple queries. |
| **Use Case Suitability**   | Ideal for live data and alerts. | Best for CRUD operations. | Good for complex queries, less suited for real-time without subscriptions. |

### Conclusion

WebSockets are essential for real-time communication in the **POT** application, allowing immediate updates and alerts that enhance health monitoring for elderly users. Unlike REST and GraphQL, WebSockets support a persistent connection and bidirectional data flow, making them suitable for applications that require instant communication and quick interventions.


## Section 3: Technology Recommendation and Justification

For the **POT** (平安通) health monitoring application, I recommend a **hybrid approach** using **REST APIs** for data management and **WebSockets** for real-time communication. And currently the company using this structure.

### Justification for the Hybrid Approach

1. **Data Complexity**:
   - **REST APIs** provide a clear structure for managing user data, simplifying CRUD operations, which is essential for health records.
   - **WebSockets** enable real-time updates from wearable devices, enhancing user interaction without added complexity.

2. **Real-time Requirements**:
   - WebSockets excel in providing instant notifications and alerts for abnormal health conditions, crucial for timely interventions.

3. **Scalability**:
   - REST APIs can scale efficiently by adding new endpoints, while WebSockets can handle many concurrent connections, supporting a growing user base.

4. **Ease of Use for Developers**:
   - REST's simplicity is familiar to many developers, facilitating faster implementation. While WebSockets introduce complexity, they are manageable with existing libraries.

### Conclusion

This hybrid approach balances structured data management with robust real-time capabilities, optimizing performance and scalability. It ensures that users receive timely alerts and updates, making it ideal for the health monitoring needs of elderly citizens. 