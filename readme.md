# Docker Voting App Example

A simple distributed voting application built with Docker Compose, allowing users to vote between two options.

## Architecture Overview

The application consists of 5 containers:
- A Python web app for casting votes
- A Redis queue to collect votes
- A .NET worker to process votes
- A PostgreSQL database to store results
- A Node.js web app to display results

## Prerequisites

- Docker Engine 20.10.0+
- Docker Compose v2.0.0+

## Quick Start

1. Clone the repository:
```bash
gh repo clone FadyHabibKelliny/Voting-app-using-Docker-Compose
cd Voting-app-using-Docker-Compose
```

2. Start the application:
```bash
docker compose up -d
```

3. Access the applications:
- Voting interface: http://localhost:5000
- Results interface: http://localhost:5001

## Stopping the Application

```bash
docker compose down
```

To completely remove all data including the database:
```bash
docker compose down -v
```

## Project Structure

```
.
├── docker-compose.yml
├── vote/             # Python voting web app
├── result/          # Node.js results web app
└── worker/          # .NET vote processing worker
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.