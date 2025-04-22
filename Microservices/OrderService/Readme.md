# OrderService - Order Management and Payment Processing API

![Node.js](https://img.shields.io/badge/Node.js-339933.svg?style=for-the-badge&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6.svg?style=for-the-badge&logo=TypeScript&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000.svg?style=for-the-badge&logo=Express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20.svg?style=for-the-badge&logo=Apache-Kafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED.svg?style=for-the-badge&logo=Docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5.svg?style=for-the-badge&logo=Kubernetes&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D.svg?style=for-the-badge&logo=Swagger&logoColor=black)
![JWT](https://img.shields.io/badge/JSON%20Web%20Tokens-000000.svg?style=for-the-badge&logo=JSON-Web-Tokens&logoColor=white)
![Pino](https://img.shields.io/badge/Pino-00A86B.svg?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0wIDE4Yy00LjQyIDAtOC0zLjU4LTgtOHMzLjU4LTggOC04IDggMy41OCA4IDgtMy41OCA4LTggOHoiLz48cGF0aCBmaWxsPSJ3aGl0ZSIgZD0iTTEyIDZjLTMuMzEgMC02IDIuNjktNiA2czIuNjkgNiA2IDYgNi0yLjY5IDYtNi0yLjY5LTYtNi02eiIvPjwvc3ZnPg==)

## Overview

OrderService is a critical component of our delivery platform, providing comprehensive order management and payment processing capabilities. This microservice handles the entire order lifecycle from creation to delivery, integrates with payment services, and communicates order status changes to other services through Kafka messaging.

**Key Features:**

- **Order Creation**: Create delivery orders with detailed pricing and route information
- **Payment Processing**: Integrate with payment services for transaction handling
- **Order Status Management**: Track and update order status throughout the delivery lifecycle
- **Pricing Calculation**: Determine delivery costs based on distance, vehicle type, and other factors
- **Event-Driven Architecture**: Publish order events to Kafka for system-wide notifications
- **Secure API**: JWT-based authentication with role-based access control
- **Kubernetes Deployment**: Containerized and orchestrated for high availability
- **Comprehensive Documentation**: Swagger/OpenAPI for API documentation

---

## Architecture

### Microservice Integration

OrderService is designed to integrate with other microservices in your ecosystem:

| Service                 | Interaction                                             |
| ----------------------- | ------------------------------------------------------- |
| **PaymentService**      | Processes payments and refunds for orders               |
| **UserService**         | Provides user information for order association         |
| **RiderService**        | Assigns and manages riders for order delivery           |
| **LocationService**     | Provides geocoding and route calculation for deliveries |
| **AuthService**         | Validates JWT tokens for secure API access              |
| **NotificationService** | Receives order status updates via Kafka                 |

#### Data Flow

1. **Order Creation**: User creates an order with delivery details
2. **Pricing Calculation**: System calculates delivery costs based on distance and vehicle type
3. **Payment Processing**: Order is linked with payment transaction
4. **Status Updates**: Order status changes are tracked and broadcast via Kafka
5. **Delivery Assignment**: Orders are assigned to riders for fulfillment
6. **Completion/Cancellation**: Orders are marked as delivered or cancelled with appropriate payment handling

---

## Technologies

- **Backend**: Node.js with Express
- **Database**: MongoDB for order storage
- **Messaging**: Kafka for event-driven communication
- **Authentication**: JWT-based auth with role-based access
- **Documentation**: Swagger/OpenAPI for API documentation
- **Logging**: Pino for structured logging
- **Containerization**: Docker
- **Orchestration**: Kubernetes

---

## Getting Started

### Prerequisites

- Node.js (v16+)
- Docker and Docker Compose
- Kubernetes (for production)
- MongoDB instance
- Kafka cluster
- Payment service endpoint

### Quick Start

1. **Clone the repository**

```shellscript
git clone https://github.com/yourusername/OrderService.git
cd OrderService
```

2. **Install dependencies**

```shellscript
npm install
```

3. **Set up environment variables**

Copy `.env.example` to `.env` and fill in your configuration values.

4. **Start the development server**

```shellscript
npm run dev
```

5. **Access the API documentation**

Open your browser and navigate to `http://localhost:9002/api-docs`

---

## Configuration

### Environment Variables

```plaintext
# Server
PORT=9002
NODE_ENV=development
LOG_LEVEL=info

# MongoDB
DB_URL=mongodb+srv://username:password@cluster.mongodb.net/database

# Kafka Configuration
CLIENT_ID=order-service
GROUP_ID=order-service-group
BROKER_1=kafka:9092

# Payment Service
PAYMENT_SERVICE=http://payment-service/payment

# Authentication
JWT_SECRET=your_jwt_secret_key
```

---

## Project Structure

```plaintext
├── src/                    # Source code
│   ├── controllers/        # API controllers
│   │   └── order.controller.ts
│   ├── db/                 # Database configuration
│   │   ├── index.ts        # MongoDB connection
│   │   └── Models/         # Mongoose models
│   │       └── Order.ts    # Order schema
│   ├── middlewares/        # Express middleware
│   │   ├── auth.middleware.ts
│   │   └── validateReq.middleware.ts
│   ├── repository/         # Data access layer
│   │   └── order.repository.ts
│   ├── routes/             # API routes
│   │   └── order.routes.ts
│   ├── service/            # Business logic
│   │   ├── broker.service.ts
│   │   ├── notification.service.ts
│   │   ├── order.service.ts
│   │   ├── payment.service.ts
│   │   └── valuation.service.ts
│   ├── types/              # TypeScript type definitions
│   ├── utils/              # Utility functions
│   │   ├── broker/         # Kafka utilities
│   │   ├── error/          # Error handling
│   │   ├── logger/         # Logging utilities
│   │   └── response/       # Response formatting
│   ├── express-app.ts      # Express application setup
│   ├── server.ts           # Main server entry point
│   └── swagger.ts          # Swagger documentation
├── k8s/                    # Kubernetes configurations
│   ├── OrderService-configmap.yaml
│   ├── OrderService-secret.yaml
│   └── OrderService-deployment.yaml
├── docker-compose.yml      # Docker compose for local development
└── package.json            # Project dependencies
```

---

## Key Features

### Order Management

- Create delivery orders with detailed information (addresses, package details, etc.)
- Track order status throughout the delivery lifecycle
- Support for different vehicle types (BIKE, CAR, TRUCK, WALK)
- Comprehensive order history for users and riders
- Order cancellation with refund processing

### Payment Processing

- Integration with payment service for transaction handling
- Payment verification and status updates
- Refund processing for cancelled orders
- Secure payment information handling

### Pricing Calculation

- Dynamic pricing based on distance, vehicle type, and package weight
- Tax calculation and itemized pricing details
- Rider commission calculation
- Transparent pricing breakdown for users

### Event-Driven Architecture

- Kafka-based messaging for order status updates
- Real-time notifications for order events
- Decoupled communication with other microservices
- Reliable event delivery with error handling

### Caching and Performance

- Efficient database queries with proper indexing
- Structured logging for monitoring and debugging
- Error handling with appropriate status codes
- Request validation for data integrity

---

## Kubernetes Deployment

### Configuration Files

- **OrderService-configmap.yaml**: Non-sensitive configuration
- **OrderService-secret.yaml**: Sensitive data (MongoDB connection string)
- **OrderService-deployment.yaml**: Service deployment and LoadBalancer

### Deployment Steps

1. **Apply Kubernetes configurations**

```shellscript
kubectl apply -f k8s/
```

2. **Verify deployments**

```shellscript
kubectl get deployments
kubectl get pods
kubectl get services
```

3. **Access the service**

The service is exposed through a LoadBalancer. Get the external IP:

```shellscript
kubectl get services order-service
```

---

## Scalability and Resilience

- **Horizontal Scaling**: Kubernetes automatically scales pods based on CPU/memory usage
- **Resource Limits**: Configured memory and CPU limits for predictable performance
- **Health Checks**: Readiness and liveness probes for reliable operation
- **Graceful Shutdown**: Proper handling of termination signals
- **Error Handling**: Comprehensive error handling with appropriate status codes
- **MongoDB Connection Resilience**: Retry strategy for database connection failures
- **Kafka Resilience**: Robust message handling with error recovery

---

## Performance Optimizations

- **Efficient Database Queries**: Proper indexing and query optimization
- **Structured Logging**: Production-appropriate logging levels
- **Request Validation**: Early validation to prevent unnecessary processing
- **Error Classification**: Detailed error information for troubleshooting
- **Response Formatting**: Consistent API response structure
- **Selective Response Fields**: Only necessary data returned to clients

---

## Monitoring and Debugging

- **Health Check Endpoint**: `/` endpoint returns health status
- **Structured Logging**: JSON-formatted logs with request context
- **Request Tracing**: HTTP request logging with Pino
- **Error Classification**: Detailed error information for troubleshooting
- **Kafka Message Monitoring**: Logging of message publishing and consumption

---

## API Documentation

The service includes comprehensive API documentation using Swagger/OpenAPI:

- **Interactive Documentation**: Available at `/api-docs` endpoint
- **Authentication Details**: Information about required JWT tokens and scopes
- **Request/Response Examples**: Sample payloads for all endpoints
- **Error Responses**: Documentation of possible error conditions
- **Schema Definitions**: Detailed data models

### Key Endpoints

| Endpoint                              | Method | Description                  | Required Scope    |
| ------------------------------------- | ------ | ---------------------------- | ----------------- |
| `/order/create`                       | POST   | Create a new delivery order  | `order.write`     |
| `/order/cancle/:order_id`             | POST   | Cancel an existing order     | `order.write`     |
| `/order/payment`                      | POST   | Process payment for an order | `order.write`     |
| `/order/updateStatus`                 | PUT    | Update order status          | `order.write`     |
| `/order/getAllOrders/user/:user_id`   | GET    | Get all orders for a user    | `order.read`      |
| `/order/getAllOrders/rider/:rider_id` | GET    | Get all orders for a rider   | `order.read`      |
| `/order/refund`                       | POST   | Process refund for an order  | `order.write`     |
| `/`                                   | GET    | Health check endpoint        | No authentication |

---

## Troubleshooting

### Common Issues

1. **MongoDB Connection Failures**

1. Check MongoDB connection string in environment variables
1. Verify network connectivity to MongoDB instance
1. Ensure database user has appropriate permissions

1. **Kafka Connection Issues**

1. Verify Kafka broker addresses
1. Check network connectivity to Kafka cluster
1. Ensure client ID and group ID are correctly configured

1. **JWT Authentication Problems**

1. Verify JWT secret is correctly configured
1. Check token expiration and scope claims
1. Ensure client is sending token in Authorization header

1. **Payment Service Integration Errors**

1. Verify payment service endpoint is correctly configured
1. Check network connectivity to payment service
1. Ensure request format matches payment service expectations

---

## Future Enhancements

- Add support for scheduled deliveries
- Implement order bundling for efficient delivery
- Add advanced analytics for order patterns and pricing optimization
- Enhance rider assignment algorithm
- Implement customer rating system for orders
- Add support for international deliveries
- Enhance payment options with multiple providers
- Implement real-time order tracking

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.
