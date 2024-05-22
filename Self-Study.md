# Database Management Systems (DBMS).

Database Management Systems (DBMS) are software systems designed to manage databases. There are several types of DBMS, each suitable for different use cases based on their structure, capabilities, and the nature of the data they manage. The primary types of DBMS are:

__1.__ __Hierarchical DBMS__:

__(a)__ Structure: Data is organized in a tree-like structure with a single root and multiple levels of parent-child relationships.

__(b)__ Suitable for: Applications with a clear hierarchical relationship, such as organizational charts or file systems.
Example: IBM Information Management System (IMS).

__2.__ __Network DBMS__:

__(a)__ Structure: Similar to hierarchical DBMS but allows more complex relationships with multiple parent nodes (many-to-many relationships).
__(b)__ Suitable for: Applications with complex relationships such as telecommunications and networking applications.
Example: Integrated Data Store (IDS).

__3.__ __Relational DBMS (RDBMS)__:

__(a)__ Structure: Data is organized into tables (relations) with rows and columns. Each table can be linked to others using keys.

__(b)__ Suitable for: Applications requiring complex queries and transactions, such as business applications, ERP systems, and CRM systems.
Example: MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server.

__4.__ __Object-oriented DBMS (OODBMS)__:

__(a)__ Structure: Data is stored as objects, similar to object-oriented programming.
__(a)__ Suitable for: Applications with complex data and relationships, such as CAD/CAM, multimedia, and AI applications.
Example: db4o, ObjectDB.

__5.__ __NoSQL DBMS__:

__(a)__ Structure: A broad category encompassing different database models that do not follow the relational model. Includes document stores, key-value stores, wide-column stores, and graph databases.

__(b)__ Suitable for: Applications requiring scalability, flexibility, and handling of large volumes of unstructured data, such as social networks, real-time web applications, and big data analytics.
Example: MongoDB (Document Store), Redis (Key-Value Store), Cassandra (Wide-Column Store), Neo4j (Graph Database).

__6.__ __NewSQL DBMS__:

__(a)__ Structure: Combines the relational model with the scalability of NoSQL databases.

__(a)__ Suitable for: Applications requiring the consistency of RDBMS with the scalability and performance of NoSQL.
Example: Google Spanner, VoltDB.

## Difference Between Relational DBMS and NoSQL
**Relational DBMS (RDBMS)**:

__1.__ Data Model: Tabular (tables with rows and columns).<br>
__2.__ Schema: Fixed schema; predefined structure.<br>
__3.__ Transactions: Strong support for ACID (Atomicity, Consistency, Isolation, Durability) properties, making them suitable for applications requiring reliable transactions.<br>
__4.__ Scalability: Vertical scalability (scaling up by adding more power to an existing server).<br>
__5.__ Query Language: Structured Query Language (SQL) for complex queries and data manipulation.<br>
__6.__ Use Cases: Banking systems, enterprise resource planning (ERP), customer relationship management (CRM).

**NoSQL DBMS**:

__1.__ Data Model: Various models including document (JSON-like documents), key-value pairs, wide-column (rows with dynamic columns), and graph (nodes and edges).<br>
__2.__ Schema: Dynamic schema; flexible and can handle unstructured data.<br>
__3.__ Transactions: Relaxed ACID properties, often providing BASE (Basically Available, Soft state, Eventual consistency) for better performance and scalability.<br>
__4.__ Scalability: Horizontal scalability (scaling out by adding more servers).<br>
__5.__ Query Language: Varies by system; may use SQL-like languages or other query mechanisms tailored to the specific data model.<br>
__6.__ Use Cases: Social media platforms, real-time analytics, content management systems, Internet of Things (IoT).

**Example Comparison**

**MongoDB (Document Store)**:

__1.__ Data Model: Stores data in flexible, JSON-like documents.<br>
__2.__ Schema: Dynamic and flexible; allows storing complex data types.<br>
__3.__ Use Cases: Content management systems, mobile apps, real-time analytics.

**MySQL (RDBMS)**:

__1.__ Data Model: Stores data in tables with fixed schemas.<br>
__2.__ Schema: Predefined; requires defining tables and relationships upfront.<br>
__3.__ Use Cases: Traditional business applications, such as e-commerce websites and ERP systems.

## Concepts of Web Application Framework
A Web Application Framework is a software framework designed to support the development of web applications, including web services, web resources, and web APIs. Here are the core concepts in a very brief summary:

__1.__ MVC Architecture: Most frameworks follow the Model-View-Controller pattern, separating the application logic (Model), user interface (View), and user input (Controller).

__2.__ Routing: Manages URL patterns and maps them to specific handlers in the application, making it easier to manage different endpoints.

__3.__ Templating: Allows dynamic generation of HTML content using templates, which can embed application data directly into the web pages.

__4.__ Database Integration: Simplifies database operations through Object-Relational Mapping (ORM) or similar mechanisms, allowing easy interaction with databases.

__5.__ Security: Provides tools and libraries for common security tasks such as authentication, authorization, and protection against web vulnerabilities.

__6.__ Middleware: Offers a way to define a pipeline of request handlers that can modify the request or response at various points during processing.

__7.__ Session Management: Manages user sessions and state across multiple requests, allowing persistent user interactions.

__8.__ Form Handling and Validation: Simplifies processing of form data and validation of user input.

__9.__ RESTful API Support: Facilitates the creation of RESTful APIs for data exchange between the client and server.

__10.__ Scaffolding: Provides tools to generate boilerplate code for common tasks, speeding up the development process.