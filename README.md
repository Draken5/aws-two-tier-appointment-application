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

## Security Considerations

## Lessons Learned

## Future Improvements
