# Joy

## Project Overview

Joy is a comprehensive enterprise management system developed by ASOFTAKE CO., LTD. (UK), built with Spring Boot 3.5.3, Java 24, and Vue 3. It includes core features such as user management, role-based access control, department management, task scheduling, and notification management, and integrates an advanced AI-powered code generation assistant with RAG capabilities.


## Development Commands

### Backend (Spring Boot + Maven)
```bash
# Build and install dependencies
mvn clean install

# Run the application
mvn spring-boot:run

# Run with specific profile
mvn spring-boot:run -Dspring-boot.run.profiles=dev

# Run tests
mvn test

# Create JAR package
mvn package
```

### Frontend (Vue 3 + Vite)
```bash
# Change to frontend directory and install dependencies
cd web && npm install

# Start development server (http://localhost:5173)
cd web && npm run dev

# Build for production
cd web && npm run build

# Preview production build
cd web && npm run preview

# Run linting
cd web && npm run lint
```

### AI Engine (Python)
```bash
# Install Python dependencies
cd ai-engine && pip3 install -r requirements.txt

# Test AI integration
cd ai-engine && python3 test_integration.py

# Run AI engine standalone
cd ai-engine && python3 main.py
```

## Architecture & Code Structure

### Backend Architecture (Spring Boot)
- **Layered Architecture**: Controller → Service → Repository → Entity
- **Base Package**: `uk.asoftake`
- **Module Structure**: Each business module contains controller, service, Repository, entity, and vo packages
- **Security**: Spring Security with session-based authentication, custom filters and handlers
- **Database**: JPA with MySQL, Redis for session storage
- **ID Generation**: Custom Snowflake ID generator

### Key Modules
- **system**: Core user/role/menu management
- **security**: Authentication, authorization, custom handlers
- **log**: Operation and login audit logging
- **job**: Scheduled task management with dynamic scheduling
- **notify**: Notification system
- **online**: Online user tracking
- **config**: System configuration management
- **ai**: AI code generation assistant module

### Frontend Architecture (Vue 3)
- **Framework**: Vue 3 with Composition API
- **UI Components**: Element Plus
- **State Management**: Pinia
- **Routing**: Vue Router
- **HTTP Client**: Axios
- **Build Tool**: Vite

### AI Engine Architecture
The project features a cutting-edge RAG (Retrieval-Augmented Generation) system, independently developed and fully integrated by our team:
- **Vector Database**: Project code and documentation indexing
- **Smart Retrieval**: Context-aware code pattern matching
- **Code Generation**: Project-specific code generation following Joy conventions
- **Integration**: Java-Python process communication via JSON

## Configuration

### Profiles
- **Development**: `application-dev.yml` (active by default)
- **Production**: `application-prod.yml`
- **Main Config**: `application.yml`

### Key Configuration Features
- **Database**: MySQL 9.0+ with JPA
- **Cache**: Redis 7.0+ for sessions and caching
- **Server Port**: 80 (backend), 5173 (frontend dev)
- **Session Timeout**: 3600 seconds
- **AI Engine**: Python 3.8+ integration with 30s timeout

## Database Setup

```bash
# Create database
CREATE DATABASE joy DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# Import latest schema
mysql -u root -p joy < db/asoftake-joy-v1-2025-07-16.sql
```

## Coding Conventions

### Java Conventions
- **Classes**: PascalCase (e.g., `UserService`, `SysUserEntity`)
- **Methods**: camelCase (e.g., `getUserById`, `updateUserStatus`)
- **Variables**: camelCase (e.g., `userId`, `userName`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_LOGIN_ATTEMPTS`)
- **Packages**: lowercase with dots (e.g., `uk.asoftake.module.system`)

### Entity Patterns
- All entities extend `BaseEntity` (includes id, createTime, updateTime)
- Use Snowflake ID generator for primary keys
- JPA annotations for relationships and constraints
- Lombok annotations for reducing boilerplate

### Service Layer Patterns
- Interface-based service design
- Transaction boundaries at service level
- Custom exceptions for business logic errors
- Audit logging through AspectJ

### Frontend Conventions
- Vue 3 Composition API preferred
- TypeScript-style prop validation
- Pinia for centralized state management
- Element Plus component library usage
- Consistent routing patterns

## AI Integration

The project integrates a fully in-house developed AI assistant designed for intelligent and context-aware code generation:

### AI Features
- **Project-aware code generation**: Understands Joy architecture patterns
- **RAG system**: Retrieval-augmented generation with project context
- **Smart suggestions**: Code completion following project conventions
- **Quality checks**: Validates generated code against project standards

### AI Usage
- **Frontend**: Access via `/ai/assistant` route (requires menu configuration)
- **API Endpoints**: `/admin/ai/*` for chat, generation, and analysis
- **Integration**: Automatic Java-Python process communication

## API Documentation

- **Swagger UI**: `http://localhost:80/swagger-ui/index.html`
- **Knife4j**: `http://localhost:80/doc.html`
- **Actuator**: `http://localhost:80/actuator/health`

## Security Architecture

- **Authentication**: Session-based with Redis storage
- **Authorization**: Role-based access control (RBAC)
- **Session Management**: Single session per user with force logout capability
- **Audit**: Comprehensive operation and login logging
- **CSRF Protection**: Enabled for web security

## Testing

### Backend Testing
```bash
# Run all tests
mvn test

# Run specific test class
mvn test -Dtest=SomeTestClass
```

### AI Engine Testing
```bash
cd ai-engine && python3 test_integration.py
```

## Development Setup

1. **Prerequisites**: Java 24, Maven 3.8+, Node.js 23+, MySQL 9.0+, Redis 7.0+, Python 3.8+
2. **Database**: Create joy database and import schema
3. **Backend**: `mvn spring-boot:run`
4. **Frontend**: `cd web && npm run dev`
5. **AI Engine**: `cd ai-engine && pip3 install -r requirements.txt`

## Important Notes

- The system uses Chinese and English internationalization
- Redis namespace: `joy:spring` for session storage
- Default server port: 80 (configurable)
- AI engine requires Python dependencies installation
- Frontend development server runs on port 5173
- All business modules follow consistent MVC pattern

## Contact

For questions, feedback, or enterprise cooperation, please contact:

**ASOFTAKE CO., LTD. (UK)**  
- Email: info@asoftake.co.uk \ lxiaoxian@outlook.com
- Facebook: [https://www.facebook.com/ASOFTAKE](@ASOFTAKE)
- Website: [https://www.asoftake.uk](https://www.asoftake.uk)
