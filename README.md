# Python discrete event simulation for complex decision making 
A Python-based Discrete Event Simulation (DES) project using the SimPy library to model decision-making scenarios and risk profiling for project scenarios and decisions

1. Probabilistic Event Modeling: Simulates key decision events in complex projects with configurable probabilities.
2. Decision Points: This section incorporates decision points where alternative courses of action can be chosen (e.g., equipment upgrades, mitigation strategies).
3. Risk Analysis: Tracks KPIs (completion time, cost, etc.) and generates distributions to visualize the project's risk profile.
4. Scenario Exploration: Allows for easy modification of probabilities, decision choices, and external factors to evaluate their impact.

Project implemented in the jupyter notebook

Steps for running the simulations 

1. Create a yaml file based on below format, for example betting on a match ticket
```yaml
# Your YAML content goes here
   start:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 1
    scale: 2
  cost_dist: uniform
  cost_params:
    loc: 0
    scale: 0
  children:
    - chooseTicketA: 0.5
    - chooseTicketB: 0.5

chooseTicketA:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 1
    scale: 2
  cost_dist: uniform
  cost_params:
    loc: -3
    scale: 0
  children:
    - Match1AWin: 0.5
    - Match1BWin: 0.5

chooseTicketB:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 2
    scale: 2
  cost_dist: uniform
  cost_params:
    loc: -5
    scale: 0
  children:
    - Match2AWin: 0.5
    - Match2BWin: 0.5

Match1AWin:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 2
    scale: 2
  cost_dist: uniform
  cost_params:
    loc: 10
    scale: 0

Match1BWin:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 3
    scale: 3
  cost_dist: uniform
  cost_params:
    loc: -5
    scale: 0

Match2AWin:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 3
    scale: 3
  cost_dist: uniform
  cost_params:
    loc: -20
    scale: 0

Match2BWin:
  capacity: 1
  service_time_dist: uniform
  service_time_params:
    loc: 3
    scale: 3
  cost_dist: uniform
  cost_params:
    loc: 5
    scale: 0
   


