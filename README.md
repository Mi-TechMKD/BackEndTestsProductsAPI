# Products API Testing

This repository contains automated tests and supporting utilities for the **Products API**. It is built using **Java**, **JUnit**, and **RestAssured** to test various CRUD operations of the API.

## Table of Contents

* [Project Overview](#project-overview)
* [Technologies Used](#technologies-used)
* [Setup](#setup)
* [Running Tests](#running-tests)
* [Project Structure](#project-structure)
* [API Examples](#api-examples)
* [Contributing](#contributing)
* [License](#license)

## Project Overview

The goal of this project is to provide automated tests for the **Products API** endpoints. The tests cover:

* **GET** all products or single products
* **POST** create new products
* **PUT** update existing products
* **DELETE** remove products

This ensures that the API works as expected and validates request/response behavior.

## Technologies Used

* Java 24
* JUnit 4
* RestAssured (API testing library)
* Maven (build and dependency management)
* Lombok (to simplify POJO creation)

## Setup

1. Clone the repository:

```bash
git clone [https://github.com/yourusername/productsAPI.git](https://github.com/Mi-TechMKD/BackEndTestsProductsAPI.git)
cd productsAPI
```

2. Install dependencies using Maven:

```bash
mvn clean install
```

3. Make sure your IDE supports Java 24 and Lombok annotations.

## Running Tests

Run all tests using Maven:

```bash
mvn test
```

Or run specific test classes from your IDE.

## Project Structure

```
productsAPI/
│
├─ src/main/java/
│   ├─ client/               # API clients (e.g., ProductsClient.java)
│   ├─ datafactory/          # Factories to generate request data
│   ├─ models/               # POJOs for requests and responses
│   ├─ objectbuilder/        # Builders to create request bodies
│   └─ utils/                # Configuration and helper classes
│
├─ src/test/java/
│   └─ productsTests/        # JUnit test classes for API endpoints
│
└─ pom.xml                   # Maven build and dependencies

```

## API Examples

### GET All Products

```java
Response response = given()
    .baseUri(Configuration.BASE_URL_PRODUCTS)
.when()
    .get()
.then()
    .statusCode(200)
    .extract().response();
```

### POST Create Product

```java
ProductsPOST body = ProductsObjectBuilder.createBodyForProdutsPOST();
Response response = given()
    .baseUri(Configuration.BASE_URL_PRODUCTS)
    .contentType("application/json")
    .body(body)
.when()
    .post()
.then()
    .statusCode(201)
    .extract().response();
```

### PUT Update Product

```java
ProductsPUTRequest body = new ProductsPUTRequest("Updated Title", 99.99);
Response response = given()
    .baseUri(Configuration.BASE_URL_PRODUCTS + "/{id}")
    .pathParam("id", 1)
    .contentType("application/json")
    .body(body)
.when()
    .put()
.then()
    .statusCode(200)
    .extract().response();
```

### DELETE Product

```java
Response response = given()
    .baseUri(Configuration.BASE_URL_PRODUCTS + "/{id}")
    .pathParam("id", 1)
.when()
    .delete()
.then()
    .statusCode(200)
    .extract().response();
```

## Contributing

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request.

## License

This project is licensed under the MIT License.
