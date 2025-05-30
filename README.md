# rescue
## Ant Colony Optimization for Multi-Vehicle Emergency Routing

This module applies Ant Colony Optimization (ACO) to solve a multi-agent routing problem 
in an emergency response context. Vehicles (e.g., ambulances) must be dispatched to a 
set of victims and hospitals with the objective of minimizing cumulative risk scores and/or 
travel time.

### Key Components:
- **Pheromone Matrix**: Shared memory across iterations that biases routing decisions toward 
  historically effective paths.
- **Heuristic Function**: Inversely proportional to score (e.g., severity or danger), guiding 
  ants toward high-utility decisions.
- **Multi-Vehicle Coordination**: Each ant builds a complete routing plan across multiple 
  vehicles, respecting visited locations and vehicle capabilities.
- **Pheromone Update Rule**: After each iteration, pheromone levels are decayed and updated 
  based on route performance (lower score or time yields higher pheromone reinforcement).

### Use Case:
This implementation is suited for time- and risk-sensitive environments where centralized 
planning must be adaptive and coordinated across multiple agents—such as disaster response 
logistics or emergency medical services.

### Outputs:
- Best route configuration by total score
- Best route configuration by total time
- Progression tracking for both metrics over iterations
