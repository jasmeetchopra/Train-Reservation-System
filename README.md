# Train Reservation System

A console-based train reservation and management system. 
The application supports two roles —train administrators and -passengers and demonstrates core object-oriented design: abstract base classes, inheritance, polymorphism, and separation of concerns across multiple translation units.

## Features

### Admin
- Generate trains automatically with randomized routes, seat counts, schedules, and train numbers
- View the full train schedule (route, platform, distance, travel time)
- View all registered passengers across every train, or for one specific train
- Delete a train from the system

### Passenger
- Register a new customer account and log in
- Book tickets on an available train
- Cancel an existing booking
- View all trains a single user is registered for
- Search, edit, and delete user information

### Under the hood
- **Distance & travel-time calculation** between station coordinates (nautical miles, km, statute miles)
- **Random generation** of train numbers, seat counts, and destination pairs
- **Role-based access** separating admin and passenger capabilities

## Architecture

The project is organized around two abstract base classes that define interfaces,
with concrete classes implementing them:

| File | Responsibility |
|------|----------------|
| `User.*` | Application entry point (`main` → `User::run()`), main menu, banners |
| `RolesAndPermissions.*` | Admin/passenger authentication, role checks (inherits `User`) |
| `Customer.*` | Passenger data and CRUD operations; shared customer collection |
| `Train.*` | Train data, scheduler, passenger registration (inherits `TrainDistance`) |
| `TrainDistance.*` | Abstract base: distance calculation + `toString` interface |
| `TrainReservation.*` | Booking/cancellation logic and displays (inherits `DisplayClass`) |
| `DisplayClass.*` | Abstract base: display interface for users and trains |
| `RandomGenerator.*` | Random IDs, train numbers, seat counts, and destinations |

### OOP concepts demonstrated
- **Abstract classes / pure virtual functions** — `TrainDistance`, `DisplayClass`
- **Inheritance** — `Train : TrainDistance`, `TrainReservation : DisplayClass`, `RolesAndPermissions : User`
- **Polymorphism** — overridden `toString()` and `calculateDistance()`
- **Encapsulation** — private data members with public getters/setters
- **Static members** — shared collections of customers and trains

## Build & Run

There is no build file in the repo, so compile the sources directly. The entry
point (`main`) lives in `User.cpp`.

### Using g++ (Linux / macOS / MinGW on Windows)
```bash
g++ -std=c++17 -o train_system *.cpp
./train_system
```

On Windows with MinGW, the output is `train_system.exe`:
```bash
g++ -std=c++17 -o train_system *.cpp
train_system.exe
```

### Using clang
```bash
clang++ -std=c++17 -o train_system *.cpp
./train_system
```

> Requires a C++17-capable compiler (g++ 7+, clang 5+, or MSVC 2017+).

## Project Structure
```
.
├── User.{hpp,cpp}                 # Entry point + main menu
├── RolesAndPermissions.{hpp,cpp}  # Authentication & roles
├── Customer.{hpp,cpp}             # Passenger management
├── Train.{hpp,cpp}                # Train data & scheduling
├── TrainDistance.{hpp,cpp}        # Abstract: distance interface
├── TrainReservation.{hpp,cpp}     # Booking & display logic
├── DisplayClass.hpp               # Abstract: display interface
├── RandomGenerator.{hpp,cpp}      # Randomized data generation
└── README.md
```

## Usage

Run the executable and follow the on-screen menu. Admins can generate and manage
trains; passengers can register, log in, and book or cancel tickets. Banners and
prompts guide you through each step.

