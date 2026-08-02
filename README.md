# AWS Two-Tier Appointment Application Deployment & Troubleshooting

## Project Overview

This project demonstrates my progression from learning the basics of deploying an Amazon LightSail instance to deploying and troubleshooting a complete two-tier application. Building on a previous LightSail project, I expanded it into a production-style environment where I configured the cloud infrastructure, worked through deployment challenges, documented the troubleshooting process, and successfully deployed an appointment application using Linux, Flask, and a MySQL database.


## Project Goal

The goal of this project was to simulate a real-world production support environment inspired by healthcare workflows, where an application depends on backend database services to function properly. For example, if a healthcare organization experienced an issue where users were unable to access appointment information through the application, I wanted to understand how to troubleshoot the problem across different layers of the application and database environment.

This project allowed me to practice identifying issues, investigating possible causes, and resolving problems across the application, database, operating system, and cloud infrastructure layers.


## Architecture

This project uses a two-tier AWS LightSail architecture consisting of a Flask application layer and a MySQL database layer. The Flask application runs on an Ubuntu Linux server and communicates with the MySQL database to store and retrieve appointment information.

The architecture simulates a production-style environment where an application depends on backend database services. The project focused on configuring the application stack, establishing database connectivity, and troubleshooting issues across the application, operating system, and database layers.


## AWS Services Used

* **Amazon LightSail** - Used to create and host the application and database server environments.
* **Ubuntu Linux** - Used as the operating system for managing the application and database infrastructure.
* **MySQL** - Used as the backend database service to store and retrieve appointment information.
* **Flask** - Used as the web application framework for the appointment application.
* **Python** - Used for application development and backend logic.
* **SSH** - Used to securely connect to and manage the LightSail server environments.


## Application Components

### Application Server

The application layer was built using Flask and deployed on an Ubuntu Linux server hosted through AWS LightSail. The Flask application handled application logic and provided API endpoints for retrieving appointment information.

The Flask service was configured to run on all network interfaces and was validated through endpoint testing API responses using curl commands.

### Database Server

The database layer consisted of a separate MySQL server environment hosted through AWS LightSail. The database stored appointment information and provided the backend data required by the Flask application.

### Application and Database Communication

The Flask application communicated with the MySQL database to retrieve and process appointment data. Testing and troubleshooting were performed to validate communication between the application and database layers.


## Deployment Process

### Infrastructure Setup

The deployment process began by creating two AWS LightSail instances to support a two-tier application architecture. The first instance served as the application server, while the second instance was configured as the dedicated database server.

Ubuntu Linux was selected as the operating system for both environments. SSH was configured to securely access and manage the server instances. Before deploying application components, I verified system readiness by checking server health and updating required packages.

### Database Server Configuration

The database server was prepared first by installing and configuring MySQL. The database environment was created to store appointment information and support communication with the Flask application running on the application server.

### Application Server Deployment

The Flask application was deployed on the application server and configured to communicate with the MySQL database server. Application testing was performed to validate connectivity between the application and database layers.


## Troubleshooting Challenges

### Challenge 1: MySQL Installation Failure Due to Limited Memory Resources

**Issue: **
During the MySQL deployment process, the installation failed because the database server had limited memory resources available. The Lightsail instance had approximately 414 MB of memory and no configured swap space, causing the MySQL process to be terminated.

**Diagnosis: **
I reviewed system logs and identified an Out of Memory (OOM) kill event, which indicated that the server did not have enough available memory to complete the MySQL installation.

**Resolution: **
I configured a 2 GB swap file on the server to provide additional virtual memory, enabled the swap space, and verified the configuration. After increasing available memory resources, I was able to successfully complete the MySQL installation.

**Lesson Learned: **
This issue reinforced the importance of understanding cloud resource limitations and validating infrastructure requirements before deploying services with higher memory demands.

### Challenge 2: Application Unable to Connect to Database

**Issue: **
The Flask application was unable to connect to the MySQL database server and returned the error:
`Can't connect to MySQL server on '172.26.5.254:3306'`

**Diagnosis: **
I performed troubleshooting steps to identify the cause of the connection failure. I verified the application server configuration, tested database connectivity, and checked the MySQL service status using Linux system management commands.

During investigation, I used the command:

```bash
sudo systemctl status mysql
```

to verify the status of the MySQL service.

**Root Cause: **
The MySQL service had failed because the Linux operating system terminated the process due to an Out of Memory (OOM) event. The AWS LightSail database instance had limited memory resources, causing MySQL to stop running.

**Resolution: **
I implemented swap storage to provide additional memory resources and verified the available memory using:

```bash
free -h
```

After confirming the system resources were available, I restarted the MySQL service and validated database connectivity from the application server.

### Challenge 3: API JSON Serialization Error

**Issue: **
While testing the Flask API endpoint, the `GET /appointments` request returned an error indicating that the database response could not be converted into JSON format:

```
Object of type timedelta is not JSON serializable
```

**Diagnosis: **
I investigated the application response and identified that MySQL time values were being returned as Python `timedelta` objects. The Flask application was unable to directly convert these values into a JSON-compatible response.

**Resolution: **
I modified the application logic to convert database time values into JSON-compatible string formats before returning the API response.

**Validation: **
I tested the updated endpoint using:

```bash
curl http://localhost:5000/appointments
```

The API successfully returned appointment data in JSON format:

```json
[
  {
    "customer_name": "John Smith",
    "appointment_time": "10:00:00"
  }
]
```

## Security Considerations

Security considerations were applied throughout the deployment process by separating the application and database environments into two different AWS LightSail instances. This helped simulate a production-style architecture where application services and database services are managed independently.

Database access was configured to support communication between the Flask application server and MySQL database server. I created and configured database permissions for the `appointment_app` database and verified connectivity between the application and database layers.

After completing testing and validating the application functionality, I terminated the LightSail instances to prevent unnecessary resource usage and ongoing costs.


## Lessons Learned

## Future Improvements
