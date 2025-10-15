# Credit Card Statement Parser

## Overview

A web application that parses PDF credit card statements from major issuers (Chase, American Express, Citi, Capital One, Discover) and extracts structured data including card details, billing cycles, balances, and transaction history. The application provides a clean, fintech-inspired interface for uploading statements and viewing parsed results with export capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React with TypeScript for type-safe component development
- Vite as the build tool and development server
- Wouter for client-side routing (lightweight React Router alternative)
- TanStack Query (React Query) for server state management and API calls

**UI Design System:**
- shadcn/ui components based on Radix UI primitives
- Tailwind CSS for styling with custom design tokens
- Material Design principles adapted for fintech applications
- Dark mode as primary theme with light mode support
- Custom color palette emphasizing trust and clarity (blues, neutrals)
- Inter font for UI text, JetBrains Mono for financial data display

**Component Architecture:**
- Atomic design pattern with reusable UI components in `/client/src/components/ui/`
- Feature-specific components in `/client/src/components/` (upload zone, results display, parsing progress)
- Page-level components in `/client/src/pages/`
- Custom hooks in `/client/src/hooks/` for shared logic (mobile detection, toast notifications)

**State Management:**
- React Query for async state (API responses, mutations)
- React Context for theme management
- Local component state for UI interactions
- No global state management library (Redux, Zustand) - keeping it simple

### Backend Architecture

**Server Framework:**
- Express.js with TypeScript
- HTTP server for API endpoints
- Vite middleware integration for development hot-reloading

**API Design:**
- RESTful endpoint: `POST /api/parse` for PDF statement upload
- Multipart form-data handling with Multer middleware
- File size limit: 10MB
- PDF-only file validation
- JSON response format with success/error patterns

**PDF Processing:**
- Custom parser implementation in `/server/pdf-parser.ts`
- Pattern-based extraction using regex for different card issuers
- Issuer detection logic for automatic parser selection
- Transaction categorization and data normalization

**Error Handling:**
- Centralized error middleware
- Structured error responses with status codes
- Request/response logging for debugging

### Data Schema & Validation

**Schema Definition:**
- Zod schemas in `/shared/schema.ts` for runtime type validation
- Shared types between client and server via TypeScript
- Drizzle-Zod integration for database schema validation

**Data Models:**
- `ParsedStatement`: Contains issuer, card info, billing cycle, balance, transactions
- `Transaction`: Date, description, amount, optional category
- `CardIssuer`: Enum for supported credit card companies
- `ParseResponse`: API response wrapper with success flag and error handling

**Why Zod:**
- Runtime validation ensures data integrity at API boundaries
- Automatic TypeScript type inference from schemas
- Validation error messages for user feedback
- Isomorphic - works on both client and server

### External Dependencies

**Core Libraries:**
- `@neondatabase/serverless`: Serverless-optimized PostgreSQL client for Neon database
- `drizzle-orm`: Type-safe SQL ORM with migrations support
- `drizzle-kit`: CLI tool for schema management and migrations
- `pdf-parse`: PDF text extraction for statement parsing

**UI Component Libraries:**
- `@radix-ui/*`: 25+ unstyled, accessible component primitives (dialogs, dropdowns, tooltips, etc.)
- `class-variance-authority`: Type-safe variant creation for component styling
- `tailwindcss`: Utility-first CSS framework
- `cmdk`: Command palette component

**Development Tools:**
- `tsx`: TypeScript execution for development
- `esbuild`: Fast bundling for production builds
- `@replit/*`: Replit-specific plugins for development environment integration

**Form & Validation:**
- `react-hook-form`: Performant form state management
- `@hookform/resolvers`: Zod integration for form validation

**Database Strategy:**
- Drizzle ORM configured for PostgreSQL (via Neon)
- Schema-first approach with TypeScript types generated from database schema
- Migration files in `/migrations/` directory
- Current implementation uses in-memory storage (`MemStorage` class) as fallback
- Database connection string expected via `DATABASE_URL` environment variable

**API Integration:**
- Fetch API for HTTP requests
- FormData for file uploads
- No axios or other HTTP client libraries
- Custom `apiRequest` wrapper in `/client/src/lib/queryClient.ts`