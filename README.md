# InventoryService

## Overview

The **InventoryService** is a microservice responsible for managing the inventory of ingredients in a restaurant's kitchen. It ensures that the available stock of ingredients is sufficient to fulfill orders and updates inventory levels when items are used or restocked. It interacts with the **OrderService** to validate ingredient availability before confirming an order.

This service is part of the broader **Restaurant Order Management System**, designed to streamline inventory management and ensure smooth operations in restaurant chains.

## Features

- **Inventory Validation**: Checks if the required ingredients are available for a new order.
- **Stock Updates**: Updates inventory levels after an order is confirmed or an ingredient is restocked.
- **Ingredient Management**: Allows adding, updating, and removing ingredients from the inventory.
- **Event-driven Architecture**: Publishes events like `AvailabilityValidated` and `InventoryUpdated` to notify other services about inventory changes.

## Architecture

The service follows **Domain-Driven Design (DDD)** principles, with clear boundaries and responsibilities:

- **Entities**: Ingredient, Recipe
- **Value Objects**: Quantity, Unit of Measure
- **Aggregates**: Ingredient (root)
- **Repositories**: IngredientRepository, RecipeRepository
- **Domain Services**: AvailabilityValidationService, InventoryUpdateService

### Communication with Other Services

- The **InventoryService** communicates with the **OrderService** to validate ingredient availability before confirming an order.
- Events are published for other services to react to, such as `AvailabilityValidated` and `InventoryUpdated`.

## Endpoints

### Get Ingredient Availability
- **GET** `/inventory/ingredients/{ingredientId}/availability`
- **Description**: Retrieves the availability of a specific ingredient.
- **Response**: Availability status (e.g., "Available", "Out of Stock").

### Update Inventory
- **PUT** `/inventory/ingredients/{ingredientId}`
- **Description**: Updates the stock quantity for a specific ingredient.
- **Request Body**: JSON containing the updated stock information (quantity, unit of measure).
- **Response**: Updated ingredient details.

### Add Ingredient
- **POST** `/inventory/ingredients`
- **Description**: Adds a new ingredient to the inventory.
- **Request Body**: JSON containing ingredient details (name, unit of measure, quantity).
- **Response**: Newly added ingredient details.

### Remove Ingredient
- **DELETE** `/inventory/ingredients/{ingredientId}`
- **Description**: Removes an ingredient from the inventory.
- **Response**: Success or error message.

## Technologies

- **Programming Language**: Java (or your preferred language)
- **Framework**: [Spring Boot / Quarkus / Micronaut] (choose the framework based on your preference)
- **Database**: PostgreSQL (or MongoDB)
- **Messaging**: Kafka or RabbitMQ (for event-driven communication)
- **Testing**: JUnit / Mockito (or testing framework of your choice)

## Setup

### Prerequisites

- Java 11 or higher
- PostgreSQL or MongoDB (depending on your choice)
- Kafka or RabbitMQ (for event communication)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/inventory-service.git
   cd inventory-service


### Folder Structure
inventory-service/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/restaurante/inventario/
│   │   │       ├── application/           # Application logic (controllers, services)
│   │   │       │   ├── controllers/       # REST controllers (API Endpoints)
│   │   │       │   └── services/          # Application services (business orchestration)
│   │   │       ├── domain/                # Domain logic (aggregates, entities, services)
│   │   │       │   ├── entities/          # Domain entities (e.g., Ingredient, Recipe)
│   │   │       │   ├── repositories/      # Data access repositories
│   │   │       │   ├── services/          # Domain services (e.g., AvailabilityValidationService)
│   │   │       │   └── valueobjects/      # Value objects (e.g., Quantity, UnitOfMeasure)
│   │   │       ├── infrastructure/        # Infrastructure logic (persistence, messaging)
│   │   │       │   ├── persistence/       # Repository implementations (DB access)
│   │   │       │   └── messaging/         # Communication with other services (Kafka, RabbitMQ)
│   │   │       └── InventoryApplication.java   # Microservice entry point (main)
│   │   └── resources/                      # Configuration files (e.g., application.properties)
│   └── test/                              # Unit and integration tests
└── pom.xml                                 # Project configuration file (if using Maven)

