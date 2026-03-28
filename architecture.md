# Mini Shop - Architecture Overview

## System Architecture

```mermaid
graph TB
    subgraph Client["Client Layer"]
        Web["Web Browser"]
        Mobile["Mobile App"]
    end
    
    subgraph Frontend["Frontend Layer"]
        UI["User Interface"]
        Cart["Shopping Cart"]
        Auth["Authentication UI"]
    end
    
    subgraph API["API Gateway & Load Balancer"]
        Gateway["API Gateway"]
        LB["Load Balancer"]
    end
    
    subgraph Backend["Backend Services"]
        AuthService["Auth Service"]
        ProductService["Product Service"]
        OrderService["Order Service"]
        PaymentService["Payment Service"]
        UserService["User Service"]
    end
    
    subgraph Database["Data Layer"]
        UserDB["User Database"]
        ProductDB["Product Database"]
        OrderDB["Order Database"]
    end
    
    subgraph External["External Services"]
        PaymentGW["Payment Gateway"]
        EmailService["Email Service"]
        CloudStorage["Cloud Storage"]
    end
    
    subgraph Cache["Cache Layer"]
        Redis["Redis Cache"]
    end
    
    Web -->|HTTP/HTTPS| Gateway
    Mobile -->|HTTP/HTTPS| Gateway
    
    Gateway --> LB
    LB --> AuthService
    LB --> ProductService
    LB --> OrderService
    LB --> PaymentService
    LB --> UserService
    
    AuthService --> UserDB
    AuthService --> Redis
    
    ProductService --> ProductDB
    ProductService --> Redis
    ProductService --> CloudStorage
    
    OrderService --> OrderDB
    OrderService --> Redis
    
    PaymentService --> PaymentGW
    PaymentService --> OrderDB
    
    UserService --> UserDB
    UserService --> EmailService
    
    style Client fill:#e1f5ff
    style Frontend fill:#f3e5f5
    style API fill:#fff3e0
    style Backend fill:#e8f5e9
    style Database fill:#fce4ec
    style External fill:#f1f8e9
    style Cache fill:#ede7f6
```

## Components Description

### Client Layer
- **Web Browser**: Desktop/web access to mini shop
- **Mobile App**: Native mobile application for iOS and Android

### Frontend Layer
- **User Interface**: Product browsing, search, filtering
- **Shopping Cart**: Add/remove items, quantity management
- **Authentication UI**: Login, registration, profile management

### API Gateway & Load Balancer
- **API Gateway**: Central entry point, request routing, rate limiting
- **Load Balancer**: Distributes traffic across backend services

### Backend Services
- **Auth Service**: User authentication, JWT tokens, session management
- **Product Service**: Product catalog, inventory management, search
- **Order Service**: Order creation, order history, order tracking
- **Payment Service**: Payment processing, transaction management
- **User Service**: User profile, preferences, notifications

### Data Layer
- **User Database**: User accounts, profiles, passwords
- **Product Database**: Product details, categories, pricing
- **Order Database**: Orders, transactions, payment records

### Cache Layer
- **Redis Cache**: Session caching, product caching, cart caching

### External Services
- **Payment Gateway**: Stripe/PayPal integration
- **Email Service**: Order confirmations, notifications
- **Cloud Storage**: Product images, documents