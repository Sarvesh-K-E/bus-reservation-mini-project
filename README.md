# Bus Reservation System (Mini Project)

A modern, high-performance web-based Bus Reservation System built to showcase the seamless integration of a heavy-duty C++ backend with a rich interactive web frontend.

## Overview

The Bus Reservation System is designed to provide a comprehensive booking experience. It combines a sleek, responsive UI with a powerful backend engine written in C++ and compiled to WebAssembly (WASM). It supports real-time seat synchronization using Firebase, interactive 3D visualizations, and an embedded terminal for power users.

## Features

- **Blazing Fast Engine**: Core business logic is written in C++ and compiled to WebAssembly for zero-latency execution in the browser.
- **Real-Time Cloud Sync**: Firebase integration for live updates, ensuring seat availability and locks are instantly synchronized across clients.
- **Concurrent Seat Lock System**: Temporarily reserves seats (30-300 seconds) during the booking flow to prevent double-booking by concurrent users.
- **Modern Interactive UI**: A premium dark-mode interface featuring micro-animations, glassmorphism, and a custom design system.
- **3D Environment**: Incorporates an immersive visual environment using a live Spline 3D scene for the authentication screen.
- **Proportional Fare Algorithm**: Custom segment-based C++ algorithm calculates fare based on the ratio of chosen segments to the total route length.
- **Power Terminal**: Command-driven embedded CLI terminal with bi-directional synchronization with the GUI for fast bookings and diagnostics.
- **Comprehensive Admin Suite**: Complete management interface for routes, buses, stops, GPS path building, ticket purging, and live revenue reporting.
- **Interactive Route Map**: Live route path visualization with stop markers using GPS coordinates via Leaflet.js.
- **Robust Data Validation**: Strict C++ validation for dates, seat capacity, duplicates, and completion status, providing robust JSON-formatted error handling.

## Technology Stack

- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Backend/Core Logic**: C++17
- **WebAssembly Compiler**: Emscripten (used to compile C++ code into `.wasm` and `.js` wrappers)
- **Database & Auth**: Firebase (Realtime Database & Authentication)
- **3D Graphics**: Spline (Interactive Viewport using `.splinecode`)
- **Mapping**: Leaflet.js

## How It Works

1. **Authentication**: Users sign in or register via the Firebase Auth integrated frontend. The login page features a 3D Spline scene that tracks mouse movement.
2. **Core Logic via WASM**: When a user selects a route or attempts to book a seat, the JavaScript frontend communicates with the WebAssembly module (compiled from C++). The C++ engine safely handles complex tasks like fare computation based on distance and validation rules.
3. **Database Syncing**: Once the booking is validated by the WASM module, the JavaScript layer pushes the transaction to the Firebase Realtime Database. Any other user viewing the same bus will see the seat instantly marked as unavailable.
4. **Command Terminal**: Users can open the terminal tab and type text commands (e.g., `book A1`) which are parsed in JavaScript and sent to the C++ core for execution.

## Project Structure

```
├── assets/
│   ├── bg.png                 # Background image assets
│   └── scene.splinecode       # 3D Interactive Spline model
├── cpp/
│   └── reservation_system.cpp # Core C++ engine source code
├── dist/
│   ├── reservation.js         # Emscripten JS wrapper for WASM
│   └── reservation.wasm       # Compiled WebAssembly binary
├── app.js                     # Main frontend logic & Firebase integration
├── firebase-config.js         # Firebase initialization configuration
├── index.html                 # Application entry point
├── styles.css                 # Custom design tokens and styles
└── build-wasm.ps1             # PowerShell script to compile C++ to WASM
```

## Setup Instructions

To run this project locally:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/BusReservationSystem.git
   cd BusReservationSystem
   ```

2. **Configure Firebase:**
   - Create a project on [Firebase](https://firebase.google.com/).
   - Enable Authentication (Email/Password) and Realtime Database.
   - Open `firebase-config.js` and replace the placeholder values with your Firebase project credentials.

3. **Serve the application:**
   - Since the project uses WebAssembly and ES6 modules, it must be served over HTTP/HTTPS (not `file://`).
   - You can use any local web server. For example, with Python:
     ```bash
     python -m http.server 8000
     ```
   - Open `http://localhost:8000` in your browser.

4. **(Optional) Recompile WebAssembly:**
   - If you modify `cpp/reservation_system.cpp`, you will need to recompile the WASM module.
   - Install [Emscripten](https://emscripten.org/docs/getting_started/downloads.html).
   - Run the build script (requires PowerShell):
     ```powershell
     ./build-wasm.ps1
     ```
