# Culture Degree System Design

## System Overview

Culture Degree is a modern educational platform built with a microservices-ready architecture, currently deployed as a modular monolith for simplicity and cost-effectiveness.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                           Client Layer                              │
├─────────────────┬───────────────────┬──────────────────────────────┤
│   Web App       │   Mobile Web      │   Future: Native Apps       │
│   (Next.js)     │   (Responsive)    │   (React Native)            │
└────────┬────────┴───────────────────┴──────────────────────────────┘
         │
         │ HTTPS
         │
┌────────▼────────────────────────────────────────────────────────────┐
│                        CDN Layer (Vercel Edge)                      │
│  • Static Assets  • Image Optimization  • Edge Functions           │
└────────┬────────────────────────────────────────────────────────────┘
         │
         │ HTTPS
         │
┌────────▼────────────────────────────────────────────────────────────┐
│                    Application Layer (Next.js)                      │
├─────────────────────────────────────────────────────────────────────┤
│  • Server Components    • API Routes (tRPC)    • Auth (NextAuth)   │
│  • Static Generation    • Server-Side Rendering • Middleware        │
└────────┬────────────────────────────────────────────────────────────┘
         │
         │ tRPC/HTTP
         │
┌────────▼────────────────────────────────────────────────────────────┐
│                      Business Logic Layer                           │
├─────────────────────────────────────────────────────────────────────┤
│  • User Service       • Content Service      • Progress Service     │
│  • Assessment Service • Discussion Service   • Analytics Service    │
└────────┬────────────────────────────────────────────────────────────┘
         │
         │ Prisma ORM
         │
┌────────▼────────────────────────────────────────────────────────────┐
│                        Data Layer                                   │
├─────────────────┬────────────────────┬─────────────────────────────┤
│   PostgreSQL    │   Redis Cache      │   S3 Object Storage       │
│   (Primary DB)  │   (Sessions)       │   (Media Files)           │
└─────────────────┴────────────────────┴─────────────────────────────┘
```

## Key Components

### 1. Frontend (Next.js App)

**Responsibilities:**
- Server-side rendering for SEO
- Client-side interactivity
- Progressive enhancement
- Responsive design
- Offline capabilities (PWA)

**Key Features:**
- App Router for file-based routing
- Server Components for performance
- Optimistic UI updates
- Real-time progress tracking
- Accessibility (WCAG 2.1 AA)

### 2. API Layer (tRPC)

**Responsibilities:**
- Type-safe API contracts
- Request validation
- Authentication checks
- Rate limiting
- Error handling

**Key Features:**
- End-to-end TypeScript
- Automatic type inference
- Batch query optimization
- WebSocket support (future)

### 3. Business Logic Services

#### User Service
- Authentication/Authorization
- Profile management
- Preferences and settings
- Account management

#### Content Service
- Course content delivery
- Media file management
- Content versioning
- Localization support

#### Progress Service
- Progress tracking
- Completion calculations
- Learning analytics
- Streak management

#### Assessment Service
- Quiz/test delivery
- Automated grading
- Feedback generation
- Certificate issuance

#### Discussion Service
- Forum functionality
- Comment threading
- Moderation tools
- Notifications

### 4. Data Storage

#### PostgreSQL (Primary Database)
- User data
- Course content
- Progress tracking
- Transactional data

#### Redis (Cache Layer)
- Session storage
- API response caching
- Real-time data
- Rate limit counters

#### S3-Compatible Storage
- Video content
- Images and documents
- User uploads
- Backup storage

## Security Architecture

### Authentication Flow
```
User → Next.js → NextAuth → Provider → Database
                    ↓
                Session Cookie
                    ↓
              Protected Routes
```

### Security Measures
1. **Authentication**: OAuth 2.0 with JWT tokens
2. **Authorization**: Role-based access control (RBAC)
3. **Data Protection**: Encryption at rest and in transit
4. **Input Validation**: Zod schemas on all inputs
5. **Rate Limiting**: Per-user and per-IP limits
6. **CORS**: Strict origin policies
7. **CSP Headers**: Content Security Policy
8. **SQL Injection**: Parameterized queries via Prisma

## Scalability Strategy

### Phase 1: Monolith (Current)
- Single Next.js application
- Vertical scaling on Vercel
- PostgreSQL on Railway
- CDN for static assets

### Phase 2: Service Separation
- Extract heavy services (video processing)
- Add message queue (RabbitMQ/SQS)
- Implement caching layer
- Add read replicas

### Phase 3: Microservices
- Separate API gateway
- Independent service deployment
- Service mesh (Istio)
- Distributed tracing

## Performance Optimization

### Frontend
- Code splitting by route
- Lazy loading components
- Image optimization (next/image)
- Font optimization
- Bundle size monitoring

### Backend
- Database query optimization
- Connection pooling
- Response caching
- Batch operations
- Background job processing

### Infrastructure
- CDN for global distribution
- Edge functions for auth
- Database indexes
- Query result caching
- Asset compression

## Monitoring & Observability

### Application Monitoring
- Error tracking (Sentry)
- Performance monitoring (Vercel Analytics)
- User analytics (PostHog)
- Uptime monitoring (BetterStack)

### Infrastructure Monitoring
- Server metrics
- Database performance
- API response times
- Cache hit rates
- Storage usage

### Logging Strategy
```
Application Logs → Structured JSON → Log Aggregator → Alerts
                                           ↓
                                     Analytics Dashboard
```

## Deployment Strategy

### Environments
1. **Development**: Local development
2. **Preview**: Vercel preview deployments
3. **Staging**: Production-like environment
4. **Production**: Live system

### CI/CD Pipeline
```
Code Push → GitHub Actions → Tests → Build → Deploy → Health Check
                ↓                                ↓
            Code Quality                    Rollback if Failed
```

### Deployment Process
1. Automated testing (unit, integration, E2E)
2. Code quality checks (ESLint, TypeScript)
3. Security scanning
4. Build optimization
5. Progressive rollout
6. Automated rollback

## Disaster Recovery

### Backup Strategy
- Database: Daily automated backups (30-day retention)
- Media files: S3 versioning and replication
- Code: Git repository with tags
- Configuration: Infrastructure as Code

### Recovery Procedures
1. **RTO (Recovery Time Objective)**: 4 hours
2. **RPO (Recovery Point Objective)**: 24 hours
3. **Failover**: Automated DNS switching
4. **Data Recovery**: Point-in-time restoration

## Future Considerations

### Technical Debt Management
- Regular dependency updates
- Code refactoring cycles
- Performance audits
- Security reviews

### Feature Expansion
- Mobile applications
- Offline learning
- AI-powered recommendations
- Live virtual classrooms
- Blockchain certificates

### Infrastructure Evolution
- Kubernetes deployment
- Multi-region support
- GraphQL federation
- Event-driven architecture