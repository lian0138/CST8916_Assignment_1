## Introduction

"POT" (平安通) is a health monitoring project that's a joint project between the Macau government and CTM (Companhia de Telecomunicações de Macau), my previous employer. I was part of the development team, working on making this system help keep the elderly in Macau safe and healthy. We use wearable tech to keep an eye on their health in real time.

## Section 1: REST and GraphQL for Data Requests and Updates
### REST for Data Requests and Updates

In the POT, we use a REST API to handle data requests and updates between the management front-end and our microservices. Here are the main endpoints:

* GET /users/{id}
Fetches a user's info, including their health metrics and history.
* POST /users
Adds a new user when they start using the health monitor.
* PUT /users/{id}
Updates a user's health data based on new information from their wearable device.
* DELETE /users/{id}
Removes a user from the system if they stop using the device or pass away.

Using a REST API for managing data in the POT provides a straightforward and reliable way to handle user information and health metrics. It connects our front-end to the microservices efficiently, ensures the system can grow, and keeps data secure. This setup helps us deliver effective and real-time health monitoring for elderly users.

### GraphQL for Data Requests and Updates

Although we're currently using REST APIs, let's explore how **GraphQL** could enhance the **POT** health monitoring system for managing data requests and updates. With **GraphQL**, we can create a more flexible and efficient data retrieval system. Here's how it might look:

- **Queries**:
  - **Get User Information**:
    ```graphql
    query {
      user(id: "123") {
        id
        name
        healthMetrics {
          heartRate
          bloodPressure
          lastUpdated
        }
      }
    }
    ```

- **Mutations**:
  - **Add New User**:
    ```graphql
    mutation {
      addUser(name: "John Doe", age: 70) {
        id
        name
      }
    }
    ```

  - **Update Health Data**:
    ```graphql
    mutation {
      updateHealthMetrics(id: "123", heartRate: 72, bloodPressure: "120/80") {
        id
        healthMetrics {
          heartRate
          bloodPressure
          lastUpdated
        }
      }
    }
    ```

  - **Delete User**:
    ```graphql
    mutation {
      deleteUser(id: "123") {
        id
        name
      }
    }
    ```

While we're currently leveraging REST APIs for the **POT** , integrating **GraphQL** could offer greater flexibility and efficiency in data management. It allows for more precise data fetching, reduces the number of requests, and can enhance the overall developer experience. However, it's essential to weigh these benefits against the added complexity and ensure it aligns with our project's needs.


### REST vs. GraphQL: Quick Comparison

| **Aspect** | **REST** | **GraphQL** |
|------------|----------|-------------|
| **Pros**   | 1. **Simplicity:** Easy to understand and implement.<br>2. **Wide Adoption:** Lots of tools and community support. | 1. **Flexible Queries:** Fetch exactly the data you need.<br>2. **Single Endpoint:** Simplifies API management. |
| **Con**    | **Over-fetching/Under-fetching:** Can retrieve too much or too little data. | **Complexity:** Harder to set up and learn compared to REST. |

### **Conclusion**

Both REST and GraphQL have their strengths. **REST** is great for straightforward applications with well-defined data needs, benefiting from its simplicity and extensive support. **GraphQL**, on the other hand, shines when you require flexible data retrieval and more efficient communication between client and server. Choose the one that best fits your project's complexity and requirements.


## Section 2: WebSockets for Real-time Communication

### How We Use WebSockets

In our **POT (平安通)**, we use **WebSockets** to handle real-time data between wearable devices and our system.

- **Data Sync:** 
  - **Every Minute:** Wearables like smartwatches send health data to the system every minute.
  
- **Instant Alerts:**
  - **Abnormal Data:** If the device detects something unusual, it sends an alert right away.
  - **Emergency Response:** Our government monitoring center receives the alert and contacts emergency services immediately.

### WebSockets vs. REST and GraphQL

| **Feature**       | **WebSockets**                          | **REST**                      | **GraphQL**                  |
|-------------------|-----------------------------------------|-------------------------------|------------------------------|
| **Real-time**     | Yes, keeps a constant connection        | No, needs polling              | No, same as REST              |
| **Communication** | Two-way, both client and server can send data | One-way, client requests data | One-way, client requests data |
| **Best For**      | Live updates and alerts                 | Standard data operations      | Flexible data queries        |

### Conclusion

WebSockets are essential for real-time communication in the POT application, allowing immediate updates and alerts that enhance health monitoring for elderly users. Unlike REST and GraphQL, WebSockets support a persistent connection and bidirectional data flow, making them suitable for applications that require instant communication and quick interventions.


## Section 3: Technology Recommendation and Justification

### **Our Technology Choice: REST APIs + WebSockets**

For our **POT (平安通)** health monitoring system, we've built a **hybrid architecture** using **REST APIs** for data management and **WebSockets** for real-time communication.

### **Why This Combination Works**

- **Data Management with REST APIs:**
  - **Structured Operations:** REST handles standard CRUD operations efficiently, making it easy to manage user data and health records.
  - **Simplicity & Support:** Widely adopted with extensive resources, ensuring smooth development and maintenance.

- **Real-time Communication with WebSockets:**
  - **Instant Updates:** WebSockets keep a constant connection, allowing wearables to send health data every minute and send immediate alerts if something goes wrong.
  - **Two-way Communication:** Enables both the devices and the system to communicate seamlessly, crucial for timely emergency responses.

- **Scalability:**
  - **Efficient Handling:** REST APIs manage numerous requests without issues, while WebSockets maintain persistent connections without overloading the server.
  - **Flexible Growth:** Each technology can scale independently based on the system's needs.

- **Developer-Friendly:**
  - **Easy Integration:** Combining REST and WebSockets leverages the strengths of both, keeping the development process straightforward.
  - **Resource Availability:** Plenty of libraries and tools are available for both technologies, speeding up development.

### **Benefits of Our Hybrid Approach**

Our hybrid approach leverages the strengths of both **REST APIs** and **WebSockets** to optimize our system. **REST APIs** are used for the management front-end to communicate with microservices, handling everyday data tasks easily with lots of community support. Meanwhile, **WebSockets** manage communication with wearable devices, allowing us to monitor health data in real time and send instant alerts. This mix boosts performance, scales smoothly as we grow, and makes it easier for our team to develop and maintain the system.

### **Conclusion**

By combining **REST APIs** with **WebSockets**, our **POT** system effectively manages both reliable data handling and real-time communication. This hybrid approach ensures high performance, scalability, and the ability to respond instantly to critical health events, perfectly aligning with our goal of providing a safe and responsive health monitoring solution.