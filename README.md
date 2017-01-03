# DataGraft Platform

This repository contains shell start-up and configuration scripts to configure, deploy and run the DataGraft Platform as a multi-container Docker application using Docker Compose. Each microservice's release of the DataGraft Platform is published as a pre-built Docker image on the Docker Hub repository (https://hub.docker.com/u/dapaas/).

## Architecture

The DataGraft Platform consists of two main parts:

1. DataGraft
2. Grafterizer

Both of these parts have been implemented through a microservice architecture consisting of a large number of sub-components, each contained in a Docker container. The DataGraft and Grafterizer tool user interfaces have been integrated to provide a consistent user experience, whereby their connected microservices communicate with each other through REST. The individual components are illustrated in the figure below. 

![datagraft-platform](https://cloud.githubusercontent.com/assets/2796494/21607399/0bd98db8-d1b6-11e6-8f3f-6d74ba24bc98.png)

DataGraft consists of the following components:
*	[DataGraft Portal](https://github.com/datagraft/datagraft-portal): The portal serves several functions. Firstly, it provides the web-based front-end that is used by the data publishers. Internally, it implements the data model and provides object-relational mapping between it and the database back-end. It also enables the communication with the database and manages the storage of uploaded files (Docker volume, or Amazon RDS  in production). Finally, this component implements the connection to the data hosting and access services.
*	DataGraft DBMS: This component represents the database management system (PostgreSQL ) for the user data and asset catalogue. Data are stored in a separate volume (Docker volume or Amazon S3  in production).

Grafterizer has the following sub-components:
*	[Grafterizer](https://github.com/datagraft/grafterizer): Front-end component that implements the interactive GUI for data cleaning and data transformations.
*	[Grafterizer dispatch service](https://github.com/datagraft/grafterizer-dispatch-service): A server component for the Grafterizer front-end that handles request authentication on its behalf (in order to ensure security) and dispatches requests for input and output across the multiple services.
*	[Graftwerk](https://github.com/datagraft/graftwerk): A sandboxed server component that executes the data cleaning and transformation scripts that are generated by the Grafterizer front-end over the set of input data sent by the dispatcher. Graftwerk uses a proprietary load-balancing component in order to distribute the traffic coming when a larger number of users use the transformation tool. 
*	[Graftwerk cache](https://github.com/datagraft/graftwerk-cache): A FIFO cache service for the Grafterizer front-end requests to Graftwerk.
*	[Vocabulary manager](https://github.com/datagraft/vocabulary-manager): Simple RDF vocabulary management service for imported vocabularies used in the RDF mapping in the front-end. Enables searching through concepts and importing.
*	[Jarfter](https://github.com/datagraft/jarfter): A web service component for compiling executable JARs for transformations generated by the Grafterizer front end. 

## Development Team

### Core Team

- [Nikolay Nikolov](https://github.com/nvnikolov) (main contact person)
- [Antoine Pultier](https://github.com/yellowiscool)
- [Dina Sukhobok](https://github.com/dinans)
- [Brian Elvesæter](https://github.com/elvesater)
- [Titi Roman](https://github.com/dr0)
- [Steffen Dalgard](https://github.com/sdalgard)

### Contributors

- [Ana Tarita](https://github.com/taritaAna)
- [Nivethika Mahasivam](https://github.com/nivemaham)
- [Dennis Gan](https://github.com/dennisgan)
- [Bjørn Marius Von Zernichow](https://github.com/bmzernichow)
- [Håvard Heitlo Holm](https://github.com/havahol)

## License

Available under the [Eclipse Public License](/LICENSE) (v1.0).
