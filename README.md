# eCommerce Products Microservice

A dedicated, production-ready microservice for managing product catalogs in a distributed eCommerce ecosystem. This repository contains both a high-performance, containerized C# .NET 8 Backend API and a modern Angular 21 Administrative Frontend.

---

## 🏗| Architecture & Project Structure

The project is structured following a **Layered Architecture** design for the backend, separated into distinct layers, alongside a responsive SPA frontend.

```
2.ProductsMicroServices/
├── BackEnd/                                  # C# .NET 8 Microservice
│   ├── ProductsMicroService.API/             # Presentation Layer (API endpoints & middleware)
│   ├── BusinessLogicLayer/                   # Business Logic Layer (Services, DTOs, Mappers, Validation)
│   ├── DataAccessLayer/                      # Data Access Layer (EF Core, Repositories, DbContext, Entities)
│   └── eCommerceSolution.ProductsService.sln # Visual Studio Solution File
├── FrontEnd/                                 # Angular 21 Client App
│   ├── src/                                  # Source Code (Components, Services, Models)
│   ├── package.json                          # NPM Dependencies
│   └── angular.json                          # Angular configuration
└── README.md                                 # Documentation
```

---

## 🛠| Technology Stack

### Backend
* **Runtime**: .NET 8.0 SDK
* **Architecture**: Layered Architecture
* **Database & ORM**: MySQL database with Entity Framework Core (EF Core)
* **API Paradigm**: ASP.NET Core Minimal APIs for lightweight and fast endpoint handling
* **Validation**: FluentValidation (with automatic pipeline validation)
* **Documentation**: Swagger / OpenAPI integration
* **Containerization**: Docker configuration

### Frontend
* **Framework**: Angular 21
* **Design System**: Angular Material for premium UI/UX aesthetics
* **State & Flow**: RxJS Reactive Extensions
* **Tooling**: Angular CLI

---

## 💾 Database Configuration

The backend is configured to connect to a **MySQL** database.

* **Database Name**: `ecommerceproductsdatabase`
* **Default Port**: `3306`
* **Default Connection String** (configured in [appsettings.json](file:///d:/Udemy/Harsha/MicroServices/PublishGitHup/2.ProductsMicroServices/BackEnd/ProductsMicroService.API/appsettings.json)):
  ```json
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost; Port=3306; Database=ecommerceproductsdatabase; User ID=root; Password=root"
  }
  ```

---

## 🌐 API Endpoints Specification

All backend endpoints are prefixed with `/api/products` and return standardized JSON payloads:

| Method | Endpoint | Description | Payload / Parameters |
| :--- | :--- | :--- | :--- |
| **GET** | `/api/products` | Retrieve all products | None |
| **GET** | `/api/products/search/product-id/{ProductID:guid}` | Get a product by GUID | `ProductID` in path |
| **GET** | `/api/products/search/{SearchString}` | Search by product name or category | `SearchString` in path |
| **POST** | `/api/products` | Create a new product (validates input) | `ProductAddRequest` (JSON) |
| **PUT** | `/api/products` | Update an existing product | `ProductUpdateRequest` (JSON) |
| **DELETE**| `/api/products/{ProductID:guid}` | Delete a product | `ProductID` in path |

---

## 🚀 Getting Started

### 1. Database Setup
Ensure that you have MySQL running (locally or via Docker) on port `3306` with credentials matching the connection string.
To apply migrations and initialize the schema, execute the following from the `BackEnd` directory:
```bash
dotnet ef database update --project DataAccessLayer --startup-project ProductsMicroService.API
```

### 2. Running the Backend
From the root directory, navigate to the API layer and start the server:
```bash
cd BackEnd/ProductsMicroService.API
dotnet run
```
Once started:
* The service will run locally (typically on HTTPS/HTTP ports defined in `launchSettings.json`).
* Swagger UI is available at `/swagger/index.html` to explore and test the endpoints directly.

### 3. Running the Frontend
Ensure you have **Node.js** and **Angular CLI** installed. Then, run the following commands:
```bash
cd FrontEnd
npm install
npm start
```
The application will serve locally at `http://localhost:4200/`.

---

## 🐳 Docker Deployment
A [Dockerfile](file:///d:/Udemy/Harsha/MicroServices/PublishGitHup/2.ProductsMicroServices/BackEnd/ProductsMicroService.API/Dockerfile) is included in the Web API project. To build and run the backend inside a Docker container:

```bash
# From the BackEnd directory
docker build -t ecommerce-products-api -f ProductsMicroService.API/Dockerfile .
docker run -d -p 8080:8080 -p 8081:8081 --name products-service ecommerce-products-api
```
