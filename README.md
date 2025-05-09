# 🛍️ E-Commerce CRUD API with NestJS

Welcome to the **E-Commerce CRUD API** project — developed as part of the Node.js Bootcamp (Week 3).  
This project is a hands-on experience in building a professional backend module structure using **NestJS**, implementing RESTful APIs with best practices such as DTO validation, guards, pipes, interceptors, and error handling.

---

## 📚 Summary

The goal of this project is to create a modular and maintainable backend architecture for an e-commerce system, providing basic **CRUD functionality for Users and Products**, while also integrating custom validation, formatted responses, role-based access, and error handling.

## 🏗️ System Architecture

### System Components

1. **Frontend Layer**
   - User Interface for customer interactions

2. **Backend Layer (NestJS)**
   - **Authentication Module**: Handles user authentication and authorization
   - **Users Module**: Manages user profiles and account information
   - **Products Module**: Handles product catalog and inventory
   - **Cart Module**: Manages shopping cart functionality
   - **Orders Module**: Processes and tracks customer orders
   - **Payments Module**: Handles payment processing
   - **Health Check Module**: Monitors system health

3. **Database Layer**
   - Stores all application data including users, products, orders, and transactions

4. **External Services**
   - Payment Gateway integration for processing payments

### Key Features
- User authentication and authorization
- Product management and catalog
- Shopping cart functionality
- Order processing and tracking
- Payment processing
- Health monitoring
- Database persistence

The system follows a modular architecture using NestJS framework, with clear separation of concerns and well-defined module boundaries. Each module handles its specific domain functionality while maintaining loose coupling with other modules.

---

## 📌 Quick Start
  1. Run the services with using docker.
      ```
      docker-compose up -d 
      ```
  2. For re-run the docker services
      ````
      docker-compose down
      docker-compose build nest-app
      docker-compose up -d
      ````
### ⚙️ Getting Started

#### 1- Clone and Install
```bash 
  git clone <repository-url>
  mkdir ecommerce-app
  cd ecommerce-app
  npm install 
```
#### 2-Node Modules Installation
```bash
    npm install
```
or 

// Before this file is running, please Firstly you run this command in terminal.
```npm list --depth=0 --json > deps.json```

you can only secondly run this .js file. 
```node runThisForRequirements.js```

and then 
```xargs npm install < requirements.txt```

#### 3- Start Development Server
- npm run start:dev

## 📦 Features

### ✅ CRUD Operations
- **Users**
  - Create, Read (paginated), Update, Delete
- **Products**
  - Create, Read (paginated), Update, Delete

> All list endpoints are paginated via query params:
  - http
?page=<number>&limit=<number>&sort=<field>&order=<asc|desc> 

### ✅ DTO Class
    - CreateUserDto: This is a data transfer object for creating a new user.
    - UpdateUserDto: This is a data transfer object for updating user information.
    - PaginationDto: This is a data transfer object for paging and search parameters.

#### **ValidationPipe**: 
 --> Why we use this pipe: We want to validate the all DTO's using globally this Validation Pipe. We want to filter invalid datas and authomatically type converting process.

### 🧱 Module Structure
Each feature is separated as a module. Each module contains:

- Controller
- Service
- DTO
- Entity

#### 📂 Example Module Structure
Please click  to see--> [Folder Tree](srcFolder.md)

### 🧪 Validation
Using class-validator and class-transformer:

 - Ensures required fields
 - Validates types and value formats
 - Uses DTOs (Data Transfer Objects) for input validation

### 🔠 Custom Pipe: CapitalizeNamePipe
A reusable pipe that transforms names into proper casing.

Example
Input:
```bash
{
  "firstName": "aLI",
  "lastName": "DOĞRU"
}

````
After Pipe:
```bash
{
  "firstName": "Ali",
  "lastName": "Doğru"
}

```
 
 ### 📌 Used in both UsersModule and ProductsModule.
 - File path: common/pipes/capitalize-name.pipe.ts

 #### 🛡️ Guards for Role-Based Access
Defined under the Auth Module.

 #### 👑 SuperAdminGuard

- Can delete users
 - Can update user roles

🧑‍💼 AdminGuard

- Can add, update, delete products

-> Super Admin inherits all Admin permissions.
 
 ### 🔁 Global Interceptor: TransformResponseInterceptor
Wraps successful responses into a standardized format:
```bash
{
  "success": true,
  "timestamp": "2025-04-24T12:00:00.000Z",
  "data": { ... }
}
```
File path: common/interceptors/transform-response.interceptor.ts

### ❌ Global Exception Filter
All thrown exceptions return responses in a consistent error structure:
```bash
{
  "success": false,
  "timestamp": "2025-04-24T12:00:00.000Z",
  "message": "Error message"
}
```

### 💾 Dummy Data
Included for development and testing purposes:
- dummyUsers.json → Contains 20 user records
- dummyProducts.json → Contains 100 product records


### 🔍 Example CURL Commands

### 📘 List Users (Paginated)
 - curl http://localhost:3000/users?page=1&limit=10&sort=id&order=asc

### ➕ Create a New User
  ```
    curl -X POST http://localhost:3000/users \
    -H "Content-Type: application/json" \
    -d '{"firstName":"aLi", "lastName":"YILMAZ", "email":"ali@example.com", "password":"123456", "role":"user"}'
   ```

### 📦 List Products (Sorted by Price Descending)
- curl http://localhost:3000/products?page=1&limit=10&sort=price&order=desc

### 🧰 Technologies Used
  - Node.js
  - NestJS - A progressive Node.js framework
  - TypeScript
  - class-validator / class-transformer
  - RESTful API Design
  - Custom Pipes, Guards, and Interceptors

### 👨‍💻 Developer Notes
    - Code is modularized and cleanly separated into layers (Controller-Service-DTO-Entity).
    - Pipes, Interceptors, and Filters enhance developer experience and standardization.
    - Dummy data supports rapid testing during development.

### JWT Secret Key Creating
```
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```
### 📦 Installation
  - Clone the repository
  - Run npm install
  - Create a .env file in the root folder and add your database connection string (DATABASE_URL)
 


### 📜 License
  - This project is part of a Node.js bootcamp and intended for educational use.
  - Feel free to fork and extend it as needed. ( 👨‍💻ozgebuyuktorun@outlook.com)