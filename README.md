# AlgoNova

AlgoNova is a full-stack educational platform for learning algorithms and practicing with the MyAlgo language. It combines a React frontend, a .NET API backend, and a C++ compiler/runner for the MyAlgo language engine.

## Overview

This project is designed to help students:

- learn algorithmic concepts through structured lessons
- practice in a code editor using the MyAlgo language
- execute programs in real time
- track progress and dashboard metrics
- interact with an AI-style study assistant
- manage lessons and exercises as an admin

## Tech stack

- Frontend: React + TypeScript + Vite
- Desktop option: Electron
- Backend: ASP.NET Core 8 Web API
- Auth/data: Supabase
- Language engine: C++ MyAlgo compiler/runtime

## Project structure

```text
.
├── backend/                 # ASP.NET Core API
│   ├── Controllers/         # API endpoints
│   ├── Services/            # Business logic
│   ├── DTOs/                # Request/response models
│   ├── Models/              # Config and database models
│   ├── appsettings.json     # Default backend config
│   ├── appsettings.Development.json
│   └── Program.cs           # API startup
├── frontend/                # React app
│   ├── src/                 # Application source code
│   ├── public/              # Static assets
│   ├── package.json         # Frontend scripts/deps
│   └── vite.config.ts       # Vite config
├── myalgo-engine/           # C++ compiler/runtime for MyAlgo
│   ├── src/                 # Engine source
│   ├── docs/                # Language docs
│   ├── examples/            # Sample programs
│   ├── CMakeLists.txt       # Build config
│   └── build/               # Generated build output
├── database/                # SQL schema/scripts
├── diagrams/                # Project diagrams
├── docs/                    # Project documentation
├── .gitignore
├── package-lock.json
└── README.md
```

## Features

- student dashboard and learning flow
- lesson and exercise browsing
- code execution using the MyAlgo engine
- JWT-based authentication via Supabase
- protected API endpoints with role-based authorization
- admin management screens for lessons, users, and exercises
- responsive UI and a Vite dev workflow

## Prerequisites

Before starting the app, install:

- Node.js 20+
- npm
- .NET 8 SDK
- CMake
- C++ compiler toolchain (MSVC, GCC, or Clang)
- g++ available in PATH for MyAlgo-generated program execution
- Supabase project credentials

## Backend setup

1. Open a terminal in the project root.
2. Restore NuGet packages:

```bash
cd backend
dotnet restore
```

3. Configure Supabase and the MyAlgo path in the backend settings.

The default config is in `backend/appsettings.json`:

```json
{
  "Supabase": {
    "Url": "",
    "ServiceKey": ""
  },
  "MyAlgo": {
    "CliPath": "../myalgo-engine/build/myalgo",
    "TimeoutMs": 10000
  }
}
```

Set your actual values for:

- `Supabase:Url`
- `Supabase:ServiceKey`
- `MyAlgo:CliPath` to the compiled MyAlgo binary path

For local development, you may also use `appsettings.Development.json` or environment variables.

4. Run the API:

```bash
cd backend
dotnet run
```

The backend exposes Swagger UI at:

```text
https://localhost:<port>/swagger
```

## Frontend setup

1. Install dependencies:

```bash
cd frontend
npm install
```

2. Start the development server:

```bash
npm run dev
```

This usually runs on:

```text
http://localhost:5173
```

3. Optional Electron app mode:

```bash
npm run dev:electron
```

## MyAlgo engine setup

Build the engine from the CMake project:

```bash
cd myalgo-engine
cmake -S . -B build
cmake --build build
```

On Windows, the compiled binary is typically under:

```text
myalgo-engine\build\Debug\myalgo.exe
```

On Linux/macOS, it is usually:

```text
myalgo-engine/build/myalgo
```

The backend expects this path in the config file. If the binary is moved, update `MyAlgo:CliPath` accordingly.

## Running the full app

Use these steps together:

1. Build the MyAlgo engine.
2. Update the backend `Supabase` and `MyAlgo` settings.
3. Start the backend with `dotnet run`.
4. Start the frontend with `npm run dev`.
5. Open the frontend in the browser to use the platform.

## Development notes

- the backend uses JWT validation against the Supabase auth provider
- CORS is configured for local frontend origins such as `http://localhost:5173`
- Swagger is enabled in development by default
- the API is organized around lesson, exercise, dashboard, progress, auth, and admin flows

## Useful commands

### Frontend

```bash
cd frontend
npm install
npm run dev
npm run build
npm run lint
```

### Backend

```bash
cd backend
dotnet restore
dotnet build
dotnet run
```

### MyAlgo engine

```bash
cd myalgo-engine
cmake -S . -B build
cmake --build build
```

## Documentation

Additional references are available in:

- `myalgo-engine/README.md`
- `frontend/README.md`
- `database/supabase_schema.sql`
- `database/supabase_reference.md`
- `docs/`

## License

This project is for academic and development use within the repository scope. Check the repository license files if present before public distribution or commercial reuse.

## Troubleshooting

### Backend fails because Supabase config is missing

Set the values for `Supabase:Url` and `Supabase:ServiceKey` in `backend/appsettings.json` or environment variables.

### MyAlgo execution fails

Check that:

- the binary exists at `MyAlgo:CliPath`
- the binary is executable
- `g++` is installed and available on your PATH

### Frontend cannot connect to the API

Verify that:

- the backend is running
- CORS settings allow your frontend origin
- the API base URL is correct in the frontend client configuration

## Contributing

Open a feature branch, make the change, and validate the backend build and frontend build before submitting a pull request.
