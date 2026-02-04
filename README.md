# ArogyaFirst - Healthcare Management Platform

A modern, scalable healthcare platform built with **Spring Boot microservices** (8 services), **React + TypeScript + Shadcn/UI** frontend, **MySQL** database, **Eureka** service discovery, **Spring Cloud Gateway**, and **Docker Compose** orchestration.  
Designed as a three-tier architecture demo, suitable for deployment on **AWS EKS** or any Kubernetes environment.

> **Note:** This project demonstrates microservices best practices: service discovery, API gateway routing, separated concerns (patient, doctor, pharmacy, etc.), and containerized deployment.

## Project Structure

```
ArogyaFirst/
├── backend/
│   ├── appointment-service/       # Appointments & scheduling
│   ├── discovery-server/          # Eureka Service Discovery
│   ├── doctor-service/            # Doctor profiles & management
│   ├── gateway-service/           # API Gateway (Spring Cloud Gateway)
│   ├── insurance-service/         # Insurance claims & verification
│   ├── medical-records-service/   # Patient medical history & records
│   ├── patient-service/           # Patient registration & CRUD
│   ├── pharmacy-service/          # Medications, prescriptions & inventory
│   └── init-scripts/              # SQL scripts for DB initialization
├── frontend/                      # React + Vite + TypeScript + Shadcn frontend
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
├── docker-compose.yml             # Orchestrates all services + MySQL
├── .dockerignore
├── .gitignore
└── README.md
```

## Microservices Overview

| Service                  | Port  | Description                              |
|--------------------------|-------|------------------------------------------|
| discovery-server         | 8761  | Eureka service registry & discovery      |
| gateway-service          | 8080  | API Gateway - single entry point         |
| patient-service          | 8081  | Patient registration, profiles, CRUD     |
| doctor-service           | 8082  | Doctor profiles, specialties, availability |
| pharmacy-service         | 8083  | Prescriptions, medication inventory      |
| appointment-service      | 8084  | Appointment booking, scheduling, payments|
| insurance-service        | 8085  | Insurance verification & claims          |
| medical-records-service  | 8086  | Secure medical history & records access  |
| Frontend (React)         | 5173  | Modern UI with Shadcn components         |
| MySQL                    | 3306  | Shared database                          |

All backend services are Spring Boot (Java 17+), communicating via REST through the gateway.

## Features

- **Microservices architecture** with service discovery (Eureka)
- **Centralized API Gateway** for routing & load balancing
- **Patient, Doctor, Appointment, Pharmacy, Insurance & Medical Records** management
- **Appointment booking** with payment simulation
- **Responsive React frontend** using Vite, Tailwind, Shadcn/UI, React Query, Zod, etc.
- **Dockerized** deployment with `docker-compose`
- Ready for Kubernetes (e.g., AWS EKS) scaling

## Quick Start (Docker - Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/17J/Arogyafirst.git
   cd Arogyafirst
   ```

2. **Start everything**
   ```bash
   docker-compose up -d --build
   ```

3. **Check running services**
   ```bash
   docker-compose ps
   ```

4. **View logs (if something fails)**
   ```bash
   docker-compose logs -f
   ```

5. **Access the app**
   - 🌐 **Frontend** → http://localhost:5173
   - 🔍 **Eureka Dashboard** → http://localhost:8761
   - 🚪 **API Gateway** (test endpoints) → http://localhost:8080

## API Endpoints (via Gateway)

All requests go through `http://localhost:8080`

### Patients
- `GET /api/patients` – List all patients
- `GET /api/patients/{id}` – Get patient details
- `POST /api/patients` – Register new patient
- `PUT /api/patients/{id}` – Update patient
- `DELETE /api/patients/{id}` – Remove patient

### Doctors
- `GET /api/doctors` – All doctors
- `GET /api/doctors/{id}` – Doctor by ID
- `GET /api/doctors/specialty/{specialty}` – Filter by specialty
- `POST /api/doctors` – Add doctor

### Appointments
- `GET /api/appointments` – All appointments
- `GET /api/appointments/patient/{patientId}` – Patient's appointments
- `GET /api/appointments/doctor/{doctorId}` – Doctor's schedule
- `POST /api/appointments` – Book appointment
- `PUT /api/appointments/{id}/cancel` – Cancel appointment

(Additional endpoints exist for pharmacy, insurance, medical records, and payments — explore via Swagger or Postman if enabled in services.)

## Local Development (without Docker)

### Prerequisites
- Java 17+
- Maven 3.9+
- Node.js 20+ & npm
- Docker (for MySQL)

### Steps

1. **Start MySQL**
   ```bash
   docker run -d --name arogya-mysql \
     -e MYSQL_ROOT_PASSWORD=password \
     -e MYSQL_DATABASE=arogya \
     -p 3306:3306 mysql:8.0
   ```

2. **Run backend services** (in separate terminals)
   ```bash
   # Start in this order
   cd backend/discovery-server && mvn spring-boot:run
   cd backend/gateway-service && mvn spring-boot:run
   cd backend/patient-service && mvn spring-boot:run
   cd backend/doctor-server && mvn spring-boot:run
   cd backend/pharmacy-service && mvn spring-boot:run
   cd backend/appointment-service && mvn spring-boot:run
   cd backend/insurance-server && mvn spring-boot:run
   cd backend/medical-records-service && mvn spring-boot:run
   ```

3. **Run frontend**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

4. Open http://localhost:5173

## Stopping & Cleanup

```bash
# Stop containers
docker-compose down

# Stop + remove volumes (clears DB data)
docker-compose down -v
```

## Tech Stack

- **Backend**: Spring Boot 3, Spring Cloud (Eureka, Gateway), Java 17, Maven
- **Frontend**: React 18, TypeScript, Vite, Shadcn/UI, Tailwind CSS, React Query, Zod
- **Database**: MySQL 8
- **DevOps**: Docker, Docker Compose (Kubernetes-ready)

## Contributing

Feel free to open issues or PRs for bug fixes, new features, or improvements!

Made with ❤️ for healthcare innovation.

```

