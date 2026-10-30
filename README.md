# Flowrist — Flower Delivery App

A cross-platform Flutter application for browsing, ordering, and tracking flower deliveries, backed by a .NET microservices platform (identity, catalog, cart, orders, payments, address). Originally built as a team project; this repository is an independent, actively maintained continuation.

## Overview

Flowrist lets customers browse a flower catalog, manage a cart, check out, pay, and track order status end to end. The mobile app talks to a backend of independent microservices (Identity, Catalog, Cart, Order, Payment, Address) behind an API gateway, with Firebase used for push notifications.

## My Role

I worked as a Flutter/mobile developer on the team that built this app, contributing to the mobile client within the Clean Architecture structure shared across the codebase. This repository is maintained independently going forward under my own account, with permission from the original team.

## Features

- Authentication: sign up, login, OTP verification, forgot/reset password, session management
- Product catalog browsing with pagination and image caching
- Shopping cart and checkout flow
- Address management with map-based location picking
- Order placement and order history/tracking
- Payment integration
- Push notifications (Firebase Cloud Messaging)
- Profile management
- Localization (Arabic/English) with RTL support
- Light/dark theming and responsive layouts

## Tech Stack

**Mobile (Flutter)**
- State management: `flutter_bloc`
- Dependency injection: `get_it` + `injectable`
- Networking: `dio` + `retrofit`, with interceptor-based logging
- Local/secure storage: `shared_preferences`, `flutter_secure_storage`
- Code generation: `freezed`, `json_serializable`, `build_runner`
- Routing: `go_router`
- Maps & location: `flutter_map`, `geolocator`, `geocoding`
- Push notifications: `firebase_messaging`, `firebase_core`, `flutter_local_notifications`
- Localization: `easy_localization`
- UI: `flutter_screenutil`, `flutter_svg`, `cached_network_image`, `shimmer`, `infinite_scroll_pagination`
- Testing: `flutter_test`, `mockito`, `bloc_test`

**Backend**
- .NET microservices (Identity, Catalog, Cart, Order, Payment, Address) behind an API gateway
- SQL Server, RabbitMQ (messaging), Redis
- Stripe (payments), Firebase Admin (push), SMTP (email)
- Docker Compose for local orchestration (see `FlowerApp-Backend/`)

## Architecture

The mobile app follows **Clean Architecture** with a **feature-first** folder structure:

```
lib/
├── app/            # App-level bootstrap, layout, routing
├── core/            # Shared infrastructure: DI, networking, theming, localization, errors, widgets
└── features/
    ├── auth/
    ├── cart/
    ├── address/
    ├── commerce/
    ├── notification/
    ├── order/
    ├── payment/
    ├── profile/
    └── sessions/
```

Each feature is organized into `data` / `domain` / `presentation` layers, with BLoC/Cubit driving presentation state and dependency injection wiring data sources through repositories into use cases.

## Getting Started

### Prerequisites
- Flutter SDK (see `.fvmrc` / `.metadata` for the pinned version; FVM recommended)
- A `.env` file at the project root (see `.env.example`) for runtime configuration
- Firebase project credentials (`google-services.json` for Android is already included; configure your own Firebase project if you fork this)
- Docker, for running the backend locally (see `FlowerApp-Backend/`)

### Setup

```bash
# Install Flutter dependencies
flutter pub get

# Generate code (DI, freezed, json_serializable, retrofit)
dart run build_runner build --delete-conflicting-outputs

# Run the app
flutter run
```

### Backend (optional, for local full-stack development)

```bash
cd FlowerApp-Backend
./setup.sh --recreate
```

This spins up the microservices stack via Docker Compose. Copy the generated `.env` and replace the placeholder credentials (`JWT_SECRET`, `EMAIL_USERNAME`, `EMAIL_PASSWORD`, `Stripe__SecretKey`, etc.) with your own before using it beyond local testing — **never commit real secrets to this file**.

## Testing

```bash
flutter test
```

## Provenance

This app was originally developed collaboratively by a team (originally hosted at `menna-ahmed123/Flower-App`). It is now maintained independently here with the original contributors' permission, as a standalone continuation of that work.
