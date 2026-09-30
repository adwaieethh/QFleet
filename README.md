🚢 Quantum-Inspired Green Fleet Optimization

Predict fuel first, then optimize the fleet. A software-only platform that combines physics + machine learning fuel prediction with quantum-inspired multi-objective optimization to cut fuel use, operating cost and GHG emissions in maritime and logistics fleets.

KeralAI Grand Challenge 2026 · Kochi Edition · Team A_Netguardians

	
Event	KeralAI Grand Challenge 2026, Kochi Edition
Date	07 October 2026
Venue	Jain University, Kochi Campus
Themes	Maritime & Shipping · Logistics & Transportation · Supply Chain & Operations
Knowledge & tech partner	IBM
Backed by	Kerala Startup Mission
Prize pool	₹1,25,000+
Table of Contents
Problem
Solution
How It Works
Fuel Prediction Module
Optimization Engine
Alternative-Fuel Scenarios
Tech Stack
System Architecture
Expected Impact
Feasibility, Challenges & Mitigation
Prototype Budget
Suggested Repository Structure
Getting Started
Roadmap
Team
License
Problem

Maritime and logistics industries face rising pressure to cut greenhouse gas emissions while staying efficient and cost-effective. Fuel is often 50–60% of operating cost and one of the largest environmental impacts of fleet operations.

Current pain points:

High fuel use from inefficient fleet planning
Hard to balance cost, emissions and delivery schedules
Traditional algorithms struggle with large, complex problem sizes
Fuel prediction is inaccurate when weather and cargo change
Little support for choosing the best alternative fuel
IMO pressure, while fleet decisions remain static and manual
Solution

The optimizer does not guess fuel. An ML + physics layer first predicts fuel consumption for every possible route and vessel condition. The quantum-inspired optimizer then uses those predictions as its cost function to find the best fleet configuration, speed and routes.

Industry issue	This project's answer
Inefficient fleet planning	Optimizes fleet deployment, vessel selection and cruising speed
Cost / emissions / schedule trade-offs	Multi-objective optimization of cost, emissions and schedule reliability
Large, complex search spaces	Quantum-inspired metaheuristics for stronger global search
Inaccurate fuel estimates	AI model estimates fuel across varying operating conditions
Alternative-fuel uncertainty	Compares LNG, methanol, hydrogen, ammonia and shore power
Static, manual decisions under IMO pressure	Minimizes lifecycle GHG emissions while ensuring compliance
How It Works
Ship & fleet data → Fuel prediction model → Quantum-inspired optimization → Best speed, vessel & fuel choice

Seven-stage pipeline:

Fleet & voyage data: AIS / telematics, cargo demand, weather
Preprocessing & features: speed, load, weather, fuel-type encoding
Fuel prediction module: classical ML + quantum-inspired feature map
Quantum-inspired optimization (QIEA): vessel × speed × fuel-type, multi-objective
Constraint handling & repair: capacity, deadlines, workload balance
Alternative-fuel scenarios: HFO / LNG / methanol / hydrogen / ammonia
Green fleet deployment plan: dashboard + API output

Result: lower cost and emissions, lower fuel consumption, and better speed and vessel choice.

Fuel Prediction Module

A hybrid of a physics-based layer and a data-driven layer.

Physics-based layer

m × a = F_traction − (F_roll + F_aero + F_grade)

F_roll  = Cr × m × g × cos θ
F_aero  = ½ × ρ × Cd × A × v²
F_grade = m × g × sin θ

f(t) = P(t) / (η × E_heat) + f_idle
Engine-efficiency maps convert power demand into fuel flow
Hybrids and EVs also track state-of-charge
Fuel-specific factors adjust energy and emissions (e.g. diesel ≈ 2.64 kg CO₂/L; B100 ≈ 93% of diesel energy)

Data-driven layer

Inputs: GPS speed & route, CAN-bus RPM / fuel flow / throttle, vehicle mass & payload, weather and road gradient
Models: XGBoost, LSTM and ensemble regressors, with a quantum-inspired feature map
Uncertainty: ensemble variance and Monte Carlo dropout produce confidence intervals that flow into the optimizer
Validation: k-fold cross-validation, RMSE and R²; simulated drive cycles for synthetic checks
Case-study accuracy: ≈5% RMSE of mean fuel
Optimization Engine

Pipeline: Physics fuel model → XGBoost / LSTM prediction → QUBO formulation → Quantum-inspired evolutionary algorithm (QIEA) → NSGA-II Pareto optimization → 2-opt route refinement

Objectives traded off

Fuel: minimize litres used
Emissions: CO₂, optionally NOₓ / PM
Cost: fuel plus operating cost
Time: travel time and on-time service

Constraints enforced

Vehicle capacity and payload
Fuel / battery range
Charging and refuelling stations
Delivery time windows
Driver hours and regulations
Emission limits and low-emission zones

Output: a Pareto front of plans, so planners can choose, for example, slightly more travel time in exchange for a large fuel saving.

Alternative-Fuel Scenarios

The optimizer is re-run per fuel scenario to show its effect on routes, cost and lifecycle GHG.

Fuel	Energy vs diesel	Emissions	Fleet implication
Diesel / HFO	Baseline	≈2.64 kg CO₂ per litre (diesel)	Established, dense infrastructure
Biodiesel / HVO	≈93% (B100) / ≈96% (HVO)	Lower; biogenic CO₂	Drop-in; B100 needs ~7% more volume
CNG / LNG	Much lower per litre	Lower CO₂; methane slip a concern	More frequent refuelling; regional haul
Hydrogen	1 kg H₂ ≈ 1 gallon gasoline equiv.	Zero tailpipe; lifecycle depends on H₂ source	Heavy tanks, few stations
E-fuels	Similar to diesel	Zero if renewable; energy-intensive to make	Option for legacy engines
Battery electric	High efficiency, limited range	Zero tailpipe; depends on grid mix	Needs charging stops; urban fleets

Maritime scenarios compared: HFO, LNG, methanol, hydrogen, ammonia and shore power.

Tech Stack
Layer	Technologies
Frontend	React.js · Tailwind CSS · Leaflet
Backend	Python · FastAPI
AI / ML	XGBoost · LSTM (PyTorch)
Optimization	QUBO · QIEA · NSGA-II · 2-opt
APIs	REST · WebSocket · Weather / Routing
Deployment	Docker · GitHub Actions · AWS
System Architecture

A modular cloud + edge design in two flows:

1. Ingest and prepare Vehicle / vessel telemetry → Edge gateway (filtering) → Cloud ingestion API → Data lake → Feature engineering

2. Predict, optimize, deliver Prediction service → Optimization service → Prediction & route DB → Dashboard & API → Driver apps / ERP

Design goals

Fast: routing queries solved in under 5 seconds
Secure: encryption and access control
Resilient: falls back to a classical solver if a quantum cloud solver is down
Always learning: continuous retraining as new data arrives
Expected Impact

⚠️ Illustrative results from modelling of a 50-truck courier fleet. To be validated in pilots.

Metric	Result
Fuel reduction on optimized routes	8–12% (driver tests)
Fuel saving for ~5% more travel time	−10% (one Pareto solution)
CO₂ reduction from shifting 30% of routes to CNG trucks	−25%

Benefits

Fuel efficiency: optimized vessel speed and routes, smart vessel selection by cargo and efficiency, better fleet utilization
Operating cost: lower fuel expense, efficient use of vessels, fuel and cargo capacity, lower overall operating cost
Sustainability: lower GHG emissions, support for LNG / methanol / hydrogen / ammonia, greener maritime transport
Feasibility, Challenges & Mitigation
Feasibility: software-only solution using vessel, speed, cargo and weather data with AI/ML and quantum-inspired optimization
Viability: practical, measurable benefits in fuel consumption, operating cost and GHG emissions
Challenges: data quality, complex operational constraints, fuel uncertainty, high computation needs during optimization
Mitigation: data validation, constraint handling, fuel scenario modelling, benchmarking on standard VRP / EVRPTW sets, algorithm tuning, and a classical fallback solver
Prototype Budget

Total: ₹15 Lakhs

Category	Cost (₹ Lakhs)	Scope
Software development	6.0	Frontend dashboard, backend, database and deployment
Data collection & processing	2.5	Vessel, weather, fuel and emissions datasets
AI fuel prediction model	2.5	Developing and training the ML models
Quantum-inspired optimizer	2.5	Metaheuristic design and tuning for fleet planning
Cloud infrastructure	1.5	Servers, model training, storage and hosting
Suggested Repository Structure

Adjust to match your actual code layout.

green-fleet-optimization/
├── frontend/            # React + Tailwind + Leaflet dashboard
├── backend/             # FastAPI services (prediction, optimization, API)
│   ├── prediction/      # Physics model, XGBoost, LSTM, uncertainty
│   ├── optimization/    # QUBO, QIEA, NSGA-II, 2-opt, constraint repair
│   └── scenarios/       # Alternative-fuel what-if analysis
├── data/                # Sample / synthetic datasets (no sensitive data)
├── notebooks/           # Experiments, validation, benchmarking
├── docs/                # Pitch deck, architecture diagrams
├── docker/              # Dockerfiles and compose files
├── .github/workflows/   # CI/CD (GitHub Actions)
└── README.md
Getting Started

Replace with your real commands once the code is in place.

bash
# Clone
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# Backend
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload

# Frontend (in a new terminal)
cd frontend
npm install
npm run dev

Docker (planned)

bash
docker compose up --build
Roadmap
 Data ingestion and preprocessing pipeline
 Physics-based fuel model
 XGBoost / LSTM fuel prediction with uncertainty estimates
 QUBO formulation and QIEA optimizer
 NSGA-II Pareto front + 2-opt refinement
 Constraint handling and repair
 Alternative-fuel scenario engine
 Dashboard (React + Leaflet) and REST / WebSocket API
 Benchmarking on VRP / EVRPTW sets with classical fallback solver
 Dockerization, CI/CD and AWS deployment
 Pilot validation of impact figures

Ideas for a Better Keralam · Predict smarter. Optimize globally. Sail and ship cleaner.
