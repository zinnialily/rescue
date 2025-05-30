# RESCUE: Real-world Emergency Solutions for Crisis Response Vehicle and Urgent Evacuation Routing

## Project Overview
**RESCUE** is a research project focused on developing and evaluating optimized pathway-finding solutions for emergency vehicles in disaster scenarios. Our goal is to minimize response times and risk by accounting for real-world complexities such as damaged roads, resource limitations, hospital capacities, and dynamic victim conditions.

## The Problem
Disasters introduce significant challenges to emergency medical services (EMS), including:

- **Damaged Roads**: Blocking EMS access and increasing travel times.
- **Resource Shortages**: Forcing prioritization and inefficient dispatch.
- **Hospital Overcrowding**: Leading to care delays and increased mortality.
- **Limited Specific Vehicle Routing**: Ignoring specialized vehicles like motorcycle ambulances.

## Objectives
Our solution aims to be:

- **Efficient**: Minimize response time while accounting for road damage, vehicle capabilities, and hospital capacities, prioritizing critical patients.
- **Scalable**: Perform effectively across urban, suburban, and rural environments, handling varying numbers of victims, vehicles, and damage levels.
- **Realistic**: Incorporate real-world population density, hospital data (OSMnx), and simulate road damage.
- **Safe**: Reduce vehicle breakdown risks by optimizing routes to balance response time with road safety and vehicle durability.

## Technical Approach & Methodologies

### Data Inputs
- **Location Data**: Road networks from OpenStreetMap for urban, suburban, and rural areas (e.g., Brisbane, Chicago, Plano, Mason County).
- **Road Damage**: Simulated with scores (1–10) and spatial smoothing to reflect realistic conditions (Minor, Medium, Major damage scenarios).
- **Victim Information**: Simulated victim locations and triage statuses (Red/Critical, Green/Non-critical, Unknown).
- **Temporary Hospitals**: Randomly assigned locations and capacities to model surge capacity.
- **Emergency Vehicles**:
  - Ambulances
  - Motorcycle Ambulances (MRVs)
  - Tactical Rescue Vehicles  
  Each type has distinct speed, road damage capacity, and patient capacity.

### Routing Algorithms Evaluated

#### 1. Greedy Algorithm
- **Concept**: A heuristic approach that makes locally optimal choices, prioritizing victims based on a weighted score (travel time + road damage risk), and dropping off at the nearest available hospital.
- **Implementation**: Baseline system, iteratively selecting the lowest-score unreached victim.

#### 2. Cluster-Based Routing (K-Means + Hungarian Algorithm)
- **Concept**: Combines K-Means clustering to group victims and the Hungarian Algorithm to optimally assign hospitals to these clusters. Greedy routing is applied within each cluster, with inter-cluster assistance logic.
- **Implementation**: Partitions victims, assigns hospitals, and routes vehicles within and across clusters.

#### 3. Simulated Annealing
- **Concept**: A metaheuristic optimization algorithm that starts from a Greedy solution and explores the solution space by probabilistically accepting worse solutions to escape local optima, based on a cooling schedule.
- **Implementation**: Uses `swap_routes`, `swap_order`, and `victim_change` operations to explore neighborhood solutions over 100 iterations with temperature decay.

#### 4. Ant Colony Optimization (ACO)
- **Concept**: A bio-inspired metaheuristic mimicking ant foraging behavior. "Ants" (vehicles) probabilistically construct routes based on pheromone trails and heuristic information. Pheromones are updated based on route quality, reinforcing better solutions.
- **Implementation**: Utilizes pheromone matrices for each vehicle type, probabilistic victim selection, and pheromone updates to reinforce high-quality routes.

## Key Findings

- **Algorithm Performance**:  
  Simulated Annealing consistently performed best, achieving the shortest time to reach all victims, fastest response to critical victims, and lowest average road damage score. The Greedy Algorithm was the least efficient.

- **Location Impact**:  
  Rural areas exhibited greater variability and significantly longer response times (+41.56 compared to urban areas), consistent with non-disaster EMS research.

- **Road Damage Impact**:  
  Worsening road conditions increased response times and risk, especially for all victims compared to just critical victims.

- **Triage Information**:  
  Lack of triage data significantly increased response times, especially in rural areas and minor-damage zones.

- **Temporary Hospitals**:  
  A "law of diminishing returns" was observed; beyond a certain number, more temporary hospitals provided minimal improvements.

- **Distance Metrics**:  
  Weighted score matrices outperformed simple Euclidean distance, especially in suburban and rural scenarios.

## Future Enhancements

- **Dynamic Patient Information**: Real-time updates for patient conditions and hospital statuses.
- **Real-Time Traffic & Weather**: Integration of live data to adapt routes dynamically.
- **Multi-modal Vehicles**: Incorporate helicopters and boats for access in complex terrains.
- **Real-Time Road Damage Updates**: Dynamically adjust routes as roads are cleared or repaired.
- **Further Scalability & Specialization**: Expand to broader disaster types and geographic zones.
- **Collaboration with Responders**: Incorporate real-world feedback to refine the model.

## Contributing
Contributions are welcome! Please fork the repository, open issues, or submit pull requests.

## License
This project is licensed under the **MIT License**.
