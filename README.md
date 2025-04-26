# 🏥 Patient Management System - Microservices Architecture

This project is a **cloud-native Patient Management System** built with a microservices architecture. It includes secure authentication, patient data management, billing via gRPC, real-time analytics via Kafka, and infrastructure automation for deployment on AWS using Docker and IaC.

---

## 🧩 Microservices Overview

### 1. **API Gateway**  
Centralized communication point for all microservices. Routes requests and handles CORS, throttling, etc.

- **Tech:** Spring Cloud Gateway  
- **Port:** `4004`

---

### 2. **Auth Service**  
Handles user registration, login, and JWT token generation/validation.

- **Tech:** Spring Boot + Spring Security + JWT  
- **Database:** PostgreSQL  

---

### 3. **Patient Service**  
Manages CRUD operations for patients. Acts as a Kafka producer to publish events and uses gRPC to talk to the Billing Service.

- **Tech:** Spring Boot  
- **Database:** MySQL  
- **Kafka Producer**  
- **gRPC Client**  

---

### 4. **Billing Service**  
Receives billing-related data via gRPC from the Patient Service.

- **Tech:** Spring Boot + gRPC Server  
- **Port:** `4001`

---

### 5. **Analytics Service**  
Listens to Kafka events from the Patient Service to generate analytics.

- **Tech:** Spring Boot  
- **Kafka Consumer**  
- **Port:** `4002`

---

## 🔐 Authentication Flow

- User signs up or logs in via Auth Service
- JWT token is returned
- Token is passed in headers (`Authorization: Bearer <token>`) on subsequent requests
- Token is verified before routing requests through the gateway

---

## 🐳 Dockerized Architecture

Each microservice runs in its **own Docker container** using `Docker Compose`.

### Docker Containers:
- `auth-service`
- `patient-service`
- `billing-service`
- `analytics-service`
- `api-gateway`
- `postgres`
- `kafka`

```bash
docker-compose up --build
