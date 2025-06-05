# eShop.Web Solution: Project-by-Project Documentation

---

## 1. Ordering.API
**Purpose:**  
REST API for managing orders (creation, update, status, etc.).

**Key Features:**
- Exposes endpoints for order operations.
- Uses Entity Framework Core with PostgreSQL.
- Publishes and subscribes to integration events via EventBus (RabbitMQ).
- Handles authentication and authorization.
- Registers MediatR pipeline behaviors for logging, validation, and transactions.

**Important Files:**
- `Program.cs`: App startup and DI configuration.
- `Extensions/Extensions.cs`: Registers services, repositories, event handlers, and EventBus subscriptions.
- `Application/Commands`, `Application/Behaviors`: Command handlers and pipeline behaviors.

---

## 2. Ordering.Domain
**Purpose:**  
Domain layer for the ordering context.

**Key Features:**
- Contains domain entities (Order, OrderItem, etc.).
- Defines domain events and aggregates.
- Contains repository interfaces and domain logic.

**Important Files:**
- `AggregatesModel/OrderAggregate`: Order and related domain models.
- `SeedWork/Entity.cs`: Base entity class for domain models.

---

## 3. Ordering.Infrastructure
**Purpose:**  
Infrastructure layer for the ordering context.

**Key Features:**
- Implements repositories and data access.
- Configures Entity Framework Core context.
- Handles database migrations and seeding.

**Important Files:**
- `OrderingContext.cs`: EF Core DbContext.
- `Repositories`: Implementations of domain repositories.

---

## 4. Catalog.API
**Purpose:**  
REST API for managing the product catalog.

**Key Features:**
- Exposes endpoints for catalog items, brands, and types.
- Uses Entity Framework Core with PostgreSQL.
- Publishes integration events for catalog changes.
- Supports AI features (OpenAI/Ollama) for product search and recommendations.

**Important Files:**
- `Program.cs`: App startup and DI configuration.
- `Controllers`: API endpoints for catalog operations.
- `Setup/catalog.json`: Sample catalog data.

---

## 5. Basket.API
**Purpose:**  
REST API for managing user shopping baskets.

**Key Features:**
- Exposes endpoints for basket CRUD operations.
- Integrates with gRPC for basket operations.
- Publishes events when basket is checked out.

**Important Files:**
- `Program.cs`: App startup and DI configuration.
- `Controllers`: API endpoints for basket operations.

---

## 6. WebApp
**Purpose:**  
Blazor Server web application for end-users.

**Key Features:**
- Provides the main e-commerce UI (catalog, basket, orders, etc.).
- Integrates with backend APIs via HTTP and gRPC.
- Uses authentication (OpenID Connect) and authorization.
- Subscribes to order status events via EventBus.

**Important Files:**
- `Program.cs`: App startup and DI configuration.
- `Extensions/Extensions.cs`: Registers services, EventBus, and authentication.
- `Pages`: Blazor pages for catalog, basket, orders, etc.

---

## 7. WebAppComponents
**Purpose:**  
Reusable Blazor components and shared services for the WebApp.

**Key Features:**
- Contains UI components and service abstractions.
- Used by the main WebApp for consistent UI and logic.

**Important Files:**
- `Components`: Blazor components.
- `Services`: Shared service interfaces and implementations.

---

## 8. Mobile.Bff.Shopping
**Purpose:**  
Backend-for-frontend (BFF) for mobile clients.

**Key Features:**
- Uses YARP Reverse Proxy to route requests to backend APIs.
- Adds service discovery and health checks.
- Can aggregate or transform API responses for mobile needs.

**Important Files:**
- `Program.cs`: App startup and proxy configuration.

---

## 9. EventBus
**Purpose:**  
Abstractions and base classes for event-driven communication.

**Key Features:**
- Defines `IEventBus`, `IntegrationEvent`, and handler interfaces.
- Provides extension methods for event registration.

**Important Files:**
- `Abstractions/IEventBus.cs`: Event bus interface.
- `IntegrationEvent.cs`: Base class for events.

---

## 10. EventBusRabbitMQ
**Purpose:**  
RabbitMQ implementation of the EventBus.

**Key Features:**
- Implements event publishing and subscription using RabbitMQ.
- Handles event serialization and deserialization.

**Important Files:**
- `EventBusRabbitMQ.cs`: Main implementation.
- `Extensions`: Registration helpers.

---

## 11. IntegrationEventLogEF
**Purpose:**  
Reliable event logging using Entity Framework Core.

**Key Features:**
- Implements the outbox pattern for integration events.
- Ensures events are persisted and retried if delivery fails.

**Important Files:**
- `IntegrationEventLogService.cs`: Event log logic.

---

## 12. eShop.ServiceDefaults
**Purpose:**  
Shared service registration and configuration extensions.

**Key Features:**
- Provides extension methods for common service setup (e.g., authentication, health checks, EventBus).
- Used by all APIs and services for consistent configuration.

**Important Files:**
- `Extensions`: Service registration helpers.

---

## 13. eShop.AppHost
**Purpose:**  
Orchestrator and host for running the distributed application (Aspire).

**Key Features:**
- Configures distributed application resources (OpenAI, Ollama, etc.).
- Sets up environment variables and resource dependencies for all projects.

**Important Files:**
- `Program.cs`: Main entry point for Aspire orchestration.
- `Extensions.cs`: Resource and environment configuration.

---

## 14. OrderProcessor
**Purpose:**  
Worker service for processing orders in the background.

**Key Features:**
- Runs as a .NET Worker Service.
- Subscribes to order-related events and processes them asynchronously.

**Important Files:**
- `Worker.cs`: BackgroundService implementation.

---

## 15. PaymentProcessor
**Purpose:**  
Worker service for processing payments in the background.

**Key Features:**
- Runs as a .NET Worker Service.
- Subscribes to payment-related events and processes them asynchronously.

**Important Files:**
- `Worker.cs`: BackgroundService implementation.

---

## 16. Identity.API
**Purpose:**  
Authentication and identity management using Duende IdentityServer.

**Key Features:**
- Provides OpenID Connect and OAuth2 endpoints.
- Manages user registration, login, and external authentication.
- Integrates with ASP.NET Core Identity.

**Important Files:**
- `Program.cs`: App startup and DI configuration.
- `Quickstart/Account/AccountController.cs`: Handles login/logout flows.
- `Data/ApplicationDbContext.cs`: Identity EF Core context.

---

## 17. Webhooks.API
**Purpose:**  
API for managing webhook subscriptions and notifications.

**Key Features:**
- Allows clients to register webhooks for various events.
- Publishes webhook notifications when events occur.

**Important Files:**
- `Controllers`: Webhook management endpoints.

---

## 18. WebhookClient
**Purpose:**  
Client for consuming webhooks (for testing or integration).

**Key Features:**
- Receives and processes webhook notifications.

**Important Files:**
- `Program.cs`: Webhook receiver logic.

---

## 19. Test Projects
- **Ordering.UnitTests, Ordering.FunctionalTests, Catalog.FunctionalTests, Basket.UnitTests, etc.**
  - Contain unit and functional tests for their respective domains.
  - Use xUnit, Moq, and test server infrastructure.

---

# General Notes

- **EventBus**: All APIs and worker services use the EventBus for integration events, enabling decoupled, event-driven communication.
- **Dependency Injection**: All services and handlers are registered using .NET’s built-in DI container.
- **Configuration**: Each project uses `appsettings.json` and environment variables for configuration.
- **Aspire Orchestration**: `eShop.AppHost` coordinates running all services together, including AI and external resources.

---

**This documentation provides a high-level overview of each project in the eShop.Web solution for new developers.**
