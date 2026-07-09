# Dynamic Resource Allocation - Hybrid PSO-ACO Cloud Simulation

A full-stack cloud computing resource allocation system that uses hybrid Particle Swarm Optimization (PSO) and Ant Colony Optimization (ACO) algorithms to efficiently assign cloudlets to virtual machines in a cloud environment.

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-0919F0?style=for-the-badge&logo=websocket&logoColor=white)
![CloudSim](https://img.shields.io/badge/CloudSim-1E90FF?style=for-the-badge&logo=cloud&logoColor=white)

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Running the Application](#-running-the-application)
- [Algorithm Details](#-algorithm-details)
- [Dashboard Features](#-dashboard-features)
- [Technologies Used](#-technologies-used)
- [Result Analysis](#-result-analysis)
- [Contributing](#-contributing)
- [License](#-license)

## 🌟 Overview

This project implements a cloud resource allocation system that optimizes the assignment of computational tasks (cloudlets) to virtual machines (VMs) using metaheuristic optimization algorithms. The system simulates a cloud environment using CloudSim and provides real-time monitoring through a modern web dashboard.

### Key Features

- **Hybrid PSO-ACO Optimization**: Combines the global search of PSO with the local search of ACO for optimal resource allocation
- **Real-time Monitoring**: Live WebSocket-based dashboard for simulation progress
- **Configurable Parameters**: Adjust cloudlet count, VM count, and iterations dynamically
- **Performance Metrics**: Tracks makespan, execution time, and resource utilization

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Hybrid PSO-ACO** | Combines Particle Swarm Optimization and Ant Colony Optimization |
| **CloudSim Integration** | Realistic cloud environment simulation |
| **Real-time Dashboard** | Live monitoring with WebSocket updates |
| **Responsive UI** | Built with React for modern web experience |
| **WebSocket API** | Real-time bidirectional communication |
| **Performance Metrics** | Makespan, execution time, VM utilization |

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (React/Vite)                    │
│              - Dashboard - Real-time charts                 │
│              - VM/Cloudlet configuration form               │
│              - Live logs display                            │
└─────────────────────────────────────────────────────────────┘
                            ↓ HTTP/WebSocket
┌─────────────────────────────────────────────────────────────┐
│              Backend API (Spring Boot)                      │
│              - REST endpoints                               │
│              - WebSocket endpoints                          │
│              - Simulation orchestration                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│              CloudSim Simulation Engine                     │
│              - PSO-ACO optimization                         │
│              - Datacenter, VM, Cloudlet models              │
│              - Performance metrics collection               │
└─────────────────────────────────────────────────────────────┘
```

## 📂 Project Structure

```
DynamicResourceAllocation-HSIA/
├── dashboard/                          # React Frontend
│   ├── src/
│   │   ├── App.jsx                     # Main dashboard component
│   │   ├── index.css                   # Global styles
│   │   └── main.jsx                    # Entry point
│   ├── index.html                      # HTML template
│   └── package.json                    # Dependencies
│
├── spring-boot-backend/                # Spring Boot Backend
│   ├── src/main/java/...
│   │   ├── SimulationApplication.java  # Main class
│   │   ├── SimulationConfig.java       # WebSocket config
│   │   ├── SimulationService.java      # Simulation logic
│   │   └── ...                         # WebSocket controllers
│   └── pom.xml                         # Maven dependencies
│
├── src/                                # CloudSim Simulation
│   ├── MainSimulation.java             # Entry point
│   ├── PSO.java                        # Particle Swarm Optimization
│   ├── ACO.java                        # Ant Colony Optimization
│   ├── HybridPSOACO.java               # Hybrid algorithm
│   ├── FitnessFunction.java            # Evaluation function
│   ├── HybridBroker.java               # CloudSim broker
│   └── ResultsLogger.java              # Output logging
│
├── lib/                                # External libraries
│   └── cloudsim-3.0.3-with-dependencies.jar
│
├── results/                            # Simulation output
│   └── output.csv                      # Results CSV
│
├── .gitignore                          # Git ignore rules
└── README.md                           # This file
```

## 🚀 Getting Started

### Prerequisites

- **Java 17+** (for CloudSim simulation)
- **Node.js 18+** (for React dashboard)
- **Maven 3.6+** (for Spring Boot backend - optional)

### Installation

#### 1. Clone the Repository

```bash
git clone https://github.com/deeksha-shetti/cloud-project.git
cd cloud-project
```

#### 2. Install Frontend Dependencies

```bash
cd dashboard
npm install
```

#### 3. Compile Java Files

```bash
cd ..
mkdir out
javac -encoding UTF-8 -cp "lib\cloudsim-3.0.3-with-dependencies.jar;lib\commons-math3-3.6.1.jar" -d out src\*.java
```

## 🏃 Running the Application

### Option 1: Run CloudSim Simulation Only

```bash
cd ..
java -cp "out;lib\cloudsim-3.0.3-with-dependencies.jar;lib\commons-math3-3.6.1.jar" MainSimulation
```

### Option 2: Run React Dashboard

```bash
cd dashboard
npm run dev
```

The dashboard will be available at `http://localhost:5174`

### Option 3: Full Stack (Backend + Frontend)

#### Start Spring Boot Backend

```bash
cd spring-boot-backend
mvn clean package
java -jar target/simulation-backend-1.0.0.jar
```

#### Start React Dashboard (in another terminal)

```bash
cd dashboard
npm run dev
```

## 🧠 Algorithm Details

### Particle Swarm Optimization (PSO)

- **Population**: 30 particles
- **Parameters**: 
  - Inertia weight (w): 0.7
  - Cognitive coefficient (c1): 1.5
  - Social coefficient (c2): 1.5
- **Iterations**: 50 (per phase)

### Ant Colony Optimization (ACO)

- **Population**: 30 ants
- **Parameters**:
  - Pheromone importance (α): 1.0
  - Heuristic importance (β): 2.0
  - Evaporation rate: 0.1
- **Iterations**: 50 (per phase)

### Hybrid PSO-ACO

The hybrid algorithm combines both approaches:
1. **Phase 1**: PSO for global search and initial solution
2. **Phase 2**: ACO seeded with PSO result for local refinement

### Fitness Function

The fitness function calculates the **makespan** - the total time to complete all cloudlets:

```
makespan = max(completion_time(vm_i)) for all VMs
```

## 📊 Dashboard Features

### Configuration Panel
- Adjust number of cloudlets (1-100)
- Set number of VMs (1-10)
- Configure max iterations (10-500)
- Real-time status indicator

### Live Monitoring
- Real-time WebSocket updates
- Live logs panel showing simulation progress
- Status indicators for running/completed/stopped

### Visualization
- Convergence chart for optimization progress
- Makespan visualization
- Resource allocation tracking

## 💻 Technologies Used

### Frontend
- **React 18** - UI library
- **Vite** - Build tool
- **Chart.js** - Data visualization
- **SockJS** - WebSocket client
- **STOMP** - Message protocol

### Backend
- **Spring Boot 3.2** - Web framework
- **Spring WebSocket** - Real-time communication
- **Java 17** - Programming language
- **CloudSim 3.0.3** - Cloud simulation

### Simulation
- **Particle Swarm Optimization** - Global search
- **Ant Colony Optimization** - Local search
- **CloudSim** - Cloud infrastructure modeling

## 📈 Result Analysis

The simulation outputs:

| Metric | Description |
|--------|-------------|
| **Makespan** | Total completion time of all cloudlets |
| **Execution Time** | Time taken by each cloudlet |
| **VM Allocation** | Which VM executed each cloudlet |
| **Start/Finish Times** | Precise timing for each task |

Results are saved to `results/output.csv` for further analysis.

## 🔧 Configuration

### Simulation Parameters

Default parameters (can be adjusted in `MainSimulation.java`):

- **Datacenter**: 16 PEs at 5000 MIPS each
- **Host**: 16GB RAM, 1TB storage, 10000 Mbps bandwidth
- **VMs**: 5 VMs with varying MIPS (500-2500), RAM (512-2048 MB)
- **Cloudlets**: 20 tasks with random lengths (1000-10000)

### Frontend Configuration

Default WebSocket URL: `http://localhost:8080/ws`

Update in `dashboard/src/App.jsx` if backend runs on different host/port.

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add some AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- CloudSim team for the cloud simulation framework
- React and Spring Boot communities for excellent documentation
- Open-source contributors for the optimization algorithms

## 📞 Contact

**Deeksha Shetti** - [@deeksha-shetti](https://github.com/deeksha-shetti)

Project Link: [https://github.com/deeksha-shetti/cloud-project](https://github.com/deeksha-shetti/cloud-project)

---

<p align="center">
  <b>Happy Coding! 🚀</b>
</p>
