---
name: flutter-design
description: Architect and implement enterprise-grade, SaaS-level Flutter applications using strict engineering discipline, scalable architecture, accessibility compliance, performance optimization, and mandatory test coverage. Designed for FAANG-level production systems serving millions to billions of users.
---

# Enterprise Flutter Architecture & Design Standard

This skill defines the mandatory standards for building production-grade Flutter applications intended for high-scale SaaS environments.

The objective is to deliver:

- Scalable architecture
- Long-term maintainability
- High-performance rendering
- Accessibility compliance
- Test-driven reliability
- Platform-consistent design excellence

Every implementation must meet enterprise engineering standards.

---

# 1. NON-NEGOTIABLE ENGINEERING REQUIREMENTS

## 1.1 Framework & Platform Standard

- Framework: **Flutter**
- Language: **Dart (null safety enabled)**
- Architectures allowed:
  - Clean Architecture
  - Feature-first modular architecture
  - Layered architecture

Mandatory support for:

- Android
- iOS
- Web (where applicable)
- Desktop (optional but scalable-ready)

No hybrid shortcuts.

---

## 1.2 Architectural Discipline

All implementations must follow:

### SOLID Principles

- Single Responsibility
- Open/Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

### ACID-Inspired Frontend Consistency

- Atomic widget composition
- Isolated business logic
- Predictable state flows
- Deterministic UI rendering
- Extensible, replaceable modules

### Separation of Concerns

Clear modular boundaries:

/core
/constants
/errors
/network
/utils
/theme

/features
/feature_name
/data
/datasources
/models
/repositories
/domain
/entities
/repositories
/usecases
/presentation
/pages
/widgets
/controllers

/shared
/widgets
/extensions
/helpers

/test

Requirements:

- No API calls inside widgets
- No business logic inside UI
- Usecases handle business rules
- Repository pattern mandatory
- Dependency injection required
- Feature isolation enforced
- Avoid god widgets

---

## 1.3 State Management Standards (MANDATORY)

Allowed enterprise patterns:

- Riverpod (Preferred)
- Bloc / Cubit
- Provider (only for simple modules)

Rules:

- State must be immutable
- Predictable state transitions
- UI reacts to state — never controls logic
- Side effects isolated from widgets
- No uncontrolled global state

---

## 1.4 Code Quality Standards

- Strict null safety
- No dynamic typing abuse
- Fully typed models
- Freezed or equivalent for immutable models (recommended)
- No debug prints in production
- Defensive programming mindset

Performance-safe practices:

- Const constructors wherever possible
- Minimize rebuild scope
- Use keys intentionally
- Avoid excessive widget nesting
- Lazy loading lists
- Efficient image caching
- Avoid unnecessary setState usage

Code must be readable and scalable for large teams.

---

# 2. ACCESSIBILITY & SEMANTICS (MANDATORY)

Accessibility is required for enterprise-grade apps.

## 2.1 Semantics & Structure

Use semantic widgets:

- `Semantics`
- `MergeSemantics`
- Proper labels for buttons and inputs

Requirements:

- Meaningful labels for screen readers
- Correct role definitions
- Logical navigation order
- Support VoiceOver / TalkBack

---

## 2.2 Accessibility Requirements

Must ensure:

- Keyboard navigation support (desktop/web)
- Visible focus indicators
- Screen reader compatibility
- Sufficient color contrast
- Scalable text support
- Responsive layouts

Avoid:

- Gesture-only interactions without alternatives
- Invisible interactive regions

---

# 3. MANDATORY TESTING STRATEGY

No production module may exist without tests.

## 3.1 Required Test Types

### Unit Tests

- Usecases
- Business logic
- Utilities
- Controllers / Notifiers

### Widget Tests

- Rendering correctness
- State-driven UI
- User interaction flows
- Accessibility labels

### Integration Tests

- Navigation flows
- API lifecycle validation
- Feature-level behavior

---

## 3.2 Coverage Requirements

Must test:

- Success states
- Loading states
- Error states
- Edge cases
- User interactions
- State transitions
- Repository mocks

Pattern:

- Arrange
- Act
- Assert (AAA)

Target mindset:

- Minimum 80% meaningful coverage

Tests must validate behavior — not implementation details.

---

# 4. FAANG-LEVEL DESIGN SYSTEM PHILOSOPHY

UI must feel intentional, scalable, and premium.

This is NOT template-based UI generation.

Design must reflect:

- Product maturity
- Design consistency
- Trust and clarity
- Long-term scalability

---

## 4.1 Design Direction

Before implementation, define:

### Product Context

- What problem does this app solve?
- Who are the users?
- Session frequency and duration?
- Mobile-first or cross-platform?

### Aesthetic Strategy

Choose a deliberate direction:

- Refined enterprise minimalism
- Data-first dashboard system
- High-density productivity UI
- Precision geometric layout
- Quiet luxury interface
- Industrial clarity design

Avoid:

- Generic mobile templates
- Over-animated UIs
- Trend-driven aesthetics
- Dribbble-only designs without usability

---

## 4.2 Motion & Interaction

Motion must be purposeful.

Rules:

- Prefer implicit animations
- Use animation controllers only when required
- Avoid heavy GPU usage
- Keep transitions fast and clear
- Micro-interactions should guide focus

Performance always wins over decoration.

---

## 4.3 Spatial & Visual Discipline

- Consistent spacing scale
- Grid-based layouts
- Intentional whitespace
- Strong typography hierarchy
- Elevation used meaningfully
- No visual noise

No default-looking Material screens.

---

# 5. PERFORMANCE & SCALABILITY (BILLION-USER STANDARD)

Every solution must assume:

- High traffic
- Low-end devices
- Slow networks
- Large datasets
- Continuous product iteration

Performance requirements:

- Avoid unnecessary rebuilds
- Optimize list rendering
- Use pagination/infinite scroll
- Background isolate for heavy computation
- Cache network responses
- Efficient state updates

Measure performance:

- Flutter DevTools profiling
- Frame rendering analysis
- Memory allocation tracking

---

# 6. NETWORKING & DATA LAYER STANDARDS

- Dio or enterprise-grade HTTP client
- Centralized API layer
- Typed DTO models
- Error normalization
- Retry strategies
- Request cancellation support

Never expose raw API responses directly to UI.

---

# 7. DEPENDENCY MANAGEMENT

Rules:

- Minimal dependency usage
- Avoid unstable packages
- Evaluate maintenance activity
- Wrap third-party libraries behind abstraction layers

Future replacement must be possible without large refactors.

---

# 8. SECURITY & PRODUCTION READINESS

Mandatory practices:

- Secure storage for tokens
- Input validation everywhere
- Certificate pinning (when required)
- No secrets in source code
- Environment-based configuration
- Proper logging strategy

---

# 9. STRICTLY PROHIBITED

- Business logic inside Widgets
- Massive StatefulWidgets doing everything
- Global mutable state
- Inline API calls in UI
- Unstructured navigation
- Hardcoded dimensions everywhere
- Overuse of setState
- Copy-paste architecture
- Untested modules

---

# 10. REQUIRED OUTPUT STRUCTURE

When generating implementations, always include:

1. Folder structure
2. Entities / Models
3. Data sources
4. Repository layer
5. Usecases
6. State management layer
7. UI widgets/pages
8. Theme and design system
9. Unit tests
10. Widget tests
11. Architectural explanation
12. Design rationale

---

# Implementation Philosophy

A FAANG-level Flutter SaaS application is not built on visual appeal alone.

It requires:

- Architectural clarity
- Engineering discipline
- Accessibility rigor
- Test reliability
- Performance awareness
- Intentional design systems

A scalable Flutter interface must be:

Predictable.  
Maintainable.  
Accessible.  
Testable.  
Performant.  
Production-ready.

This skill enforces that standard.
