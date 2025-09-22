# Policy Iteration in a Stochastic Environment
This project implements policy iteration in a stochastic environment using policy evaluation and policy improvement. It demonstrates how an agent can iteratively improve its strategy to maximize expected rewards in uncertain settings.

This repository contains a Python implementation of **Policy Iteration** applied to the `FrozenLake-v1` environment from OpenAI Gym. The project focuses on evaluating and improving two types of policies:

1. **Go-Get Policy**  
2. **Careful Policy**

The main goal is to analyze how different policies perform in terms of reaching the goal state under a stochastic environment.

<img width="407" height="427" alt="image" src="https://github.com/user-attachments/assets/9dc8c694-f8aa-486b-a532-5babd55cfa1a" />


---

## Project Overview

The implementation is encapsulated in the `Policy_Iteration` class, which provides the following functionalities:

### 1. Policy Evaluation
- Computes the **value function V** for a given policy using the Bellman expectation equation.
- Can generate **heatmaps** to visualize the value function over the 4x4 FrozenLake grid.
- Example usage:
```python
careful_policy_evaluation = careful_policy_search.policy_evaluation()
careful_policy_search.heatmap_policy_evaluation(careful_policy_evaluation)
```

<img width="515" height="435" alt="image" src="https://github.com/user-attachments/assets/d14bf318-92c8-4efe-bb03-4f9d30dd1fe1" />

### 2. Policy Improvement

- Uses the computed value function V to update the policy for each state.
- Returns a new policy function that selects the optimal action based on Q-values derived from V.
- Example usage:
```python
careful_policy_improvement = careful_policy_search.policy_improvement(careful_policy_evaluation)
careful_policy_search.plot_table_policy_improvement(careful_policy_improvement)
```

<img width="407" height="427" alt="image" src="https://github.com/user-attachments/assets/0645436a-e640-487a-ab7d-d4d2fde38ce3" />

### 3. Success Rate Evaluation

- Evaluates a given policy by simulating episodes in FrozenLake.
- Returns the success rate as the percentage of episodes that reach the goal.


### 4. Policy Iteration

- Automatically performs policy evaluation and policy improvement in a loop until convergence to the optimal policy.
- Example usage:
``` python
optimal_V, optimal_pi = careful_policy_search.run()
careful_policy_search.plot_table_policy_improvement(optimal_pi)
success_rate = careful_policy_search.success_rate(optimal_pi)
```

<img width="407" height="427" alt="image" src="https://github.com/user-attachments/assets/d3d63fd7-4143-4ff3-aebb-dba710f8d296" />

### 5. Results

- The project compares two policies:

1. Go-Get Policy: Aggressive strategy aiming directly for the goal.

2. Careful Policy: More conservative strategy avoiding holes.

- Success rates observed (may vary due to stochasticity of FrozenLake):

1. Go-Get Policy: 73.34%

2. Careful Policy: ~73.92%

<img width="695" height="451" alt="image" src="https://github.com/user-attachments/assets/d2f71fcb-acf7-47bd-9735-b416b2982e45" />


### 6. How to Run

1. Install dependencies:
```python
 pip install gym numpy seaborn matplotlib
```
2.Load the FrozenLake-v1 environment and initialize the class:
```python
env = gym.make('FrozenLake-v1', is_slippery=True)
P = env.env.env.env.P
```
3. Run policy evaluation, improvement, or full policy iteration as needed.


#### Notes
- The stochastic nature of FrozenLake can cause slight variations in success rates between runs. Increasing the number of episodes in success_rate() reduces variance.

- Heatmaps and policy grids provide intuitive visualizations for policy analysis.
