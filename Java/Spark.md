# Overview
* Spark was originally inspired by the web framework Sinatra. 
* Spark is built around Java 8's lambda philosophy, which makes a typical Spark application a lot less verbose than most application written in other Java web frameworks. 
* 2015 was the year of microservice hype, Spark is great for microservices. Microservices work best with micro frameworks, and Spark has your REST API ready to serve JSON in less than ten lines of code. 

# Routes
The main building block of a Spark application is a set of routes. A route is made up of three simple pieces:
* A **verb** (get, post, put, delete, head, trace, connect, options)
* A **path** (/hello, /users/:name)
* A **callback** (request, response) -> { }
