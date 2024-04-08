# Python discrete event simulation for complex decision making 
A Python-based Discrete Event Simulation (DES) project using the SimPy library to model decision-making scenarios and risk profiling for project scenarios and decisions

1. Probabilistic Event Modeling: Simulates key decision events in complex projects with configurable probabilities.
2. Decision Points: This section incorporates decision points where alternative courses of action can be chosen (e.g., equipment upgrades, mitigation strategies).
3. Risk Analysis: Tracks KPIs (completion time, cost, etc.) and generates distributions to visualize the project's risk profile.
4. Scenario Exploration: Allows for easy modification of probabilities, decision choices, and external factors to evaluate their impact.

Project implemented in the jupyter notebook

Steps for running the simulations 

1. Create a yaml file based on below format, for example, betting on a match ticket

![Alt text](https://github.com/Asad1287/decision_trees_simulations/blob/main/image.JPG "Optional title")

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


2. Load the yaml file and run the following script to start the simulation and generate results

def load_resource_config(file_path):
    with open(file_path, 'r') as file:
        config = yaml.safe_load(file)

    resource_configs = {}
    for resource_name, resource_data in config.items():
        children = [(child_name, probability) for child_data in resource_data.get('children', []) for child_name, probability in child_data.items()]
        resource_configs[resource_name] = {
            'capacity': resource_data['capacity'],
            'service_time_dist': resource_data['service_time_dist'],
            'service_time_params': resource_data['service_time_params'],
            'cost_dist': resource_data['cost_dist'],
            'cost_params': resource_data['cost_params'],
            'children': children
        }

    return resource_configs

if __name__ == "__main__":
    num_simulations = 10
    num_entities_per_sim = 1
    file_path = 'simulation.yaml'
    resource_configs = load_resource_config(file_path)

    entry_point = 'start'
    inter_arrival_time_dist = Distribution('uniform', {'loc': 0, 'scale': 5})

    runner = Runner(num_simulations, num_entities_per_sim, resource_configs, entry_point, EntityItem, inter_arrival_time_dist)
    runner.run_simulations()
   


