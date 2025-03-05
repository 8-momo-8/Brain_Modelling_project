# Neural Models Analysis Project

## Overview
This project provides a comprehensive framework for analyzing and simulating neural models, focusing on:
- Single neuron dynamics
- Network-level interactions
- Advanced analysis techniques

The implementation includes two primary neuron models (FitzHugh-Nagumo and Izhikevich) and tools for network simulation and analysis.

## Table of Contents
1. [Single Neuron Models](#single-neuron-models)
   - [FitzHugh-Nagumo Model](#fitzhugh-nagumo-model)
   - [Izhikevich Model](#izhikevich-model)
2. [Network Implementation](#network-implementation)
3. [Analysis Methods](#analysis-methods)
4. [Visualization Tools](#visualization-tools)
5. [Usage](#usage)
6. [Parameters](#parameters)
7. [Mathematical Background](#mathematical-background)
8. [References](#references)

## Single Neuron Models

### FitzHugh-Nagumo Model
The FitzHugh-Nagumo (FHN) model is a simplified representation of neuronal activity, capturing the essential features of action potential generation. The model consists of two variables:
- v: Membrane potential
- w: Recovery variable

#### Key Equations
```
dv/dt = v - v³/3 - w + I_ext
dw/dt = (v + a - b*w)/c
```

#### Parameters
- a, b, c: Model constants
- I_ext: External current input

#### Analysis Features
- Phase plane analysis
- Nullcline visualization
- Oscillation frequency calculation
- Stability metrics

### Izhikevich Model
The Izhikevich model provides a computationally efficient yet biologically plausible representation of neuronal dynamics. It can reproduce various firing patterns observed in real neurons.

#### Key Equations
```
dv/dt = 0.04v² + 5v + 140 - u + I
du/dt = a(bv - u)
if v ≥ 30 mV, then v ← c, u ← u + d
```

#### Parameters
- a, b, c, d: Model parameters controlling dynamics
- I: Input current

#### Analysis Features
- Spike train analysis
- Firing pattern classification
- Interspike interval statistics
- Burst detection

## Network Implementation
The network implementation creates interconnected networks of Izhikevich neurons with:
- Configurable network size (N)
- Probabilistic connectivity (p_connect)
- Excitatory/inhibitory neuron ratio
- Directed synaptic connections

### Network Features
- Customizable connection weights
- Population dynamics analysis
- Synchronization metrics
- Network topology visualization

## Analysis Methods
The project includes several analysis tools:

### Spike Train Analysis
- Interspike interval (ISI) calculation
- Coefficient of variation (CV)
- Firing rate estimation

### Phase Plane Analysis
- Nullcline computation
- Vector field visualization
- Trajectory plotting

### Network Analysis
- Population activity metrics
- Synchronization index
- Clustering coefficient
- Degree distribution

## Visualization Tools
The project provides comprehensive visualization capabilities:

### Single Neuron Visualizations
- Membrane potential time series
- Phase plane plots
- Nullcline visualization

### Network Visualizations
- Raster plots
- Population activity plots
- Network topology graphs
- ISI histograms

## Usage
To use the project:

1. Import required classes:
```python
from neural_models import FitzhughNagumo, IzhikevichNeuron, NeuralNetwork
```

2. Create and simulate models:
```python
# FitzHugh-Nagumo
fn = FitzhughNagumo(a=0.7, b=0.8, c=12.5, I_ext=0.5)
t, sol = fn.simulate(T=200)

# Izhikevich
izh = IzhikevichNeuron(a=0.02, b=0.2, c=-65, d=8)
[izh.step(10) for _ in range(1000)]

# Network
net = NeuralNetwork(N=100, p_connect=0.1)
time, activity = net.simulate(T=500)
```

3. Analyze and visualize results:
```python
# Single neuron analysis
fn.explain_results(t, sol)
izh.analyze_behavior()

# Network analysis
net.analyze_network(time, activity)
plot_network_analysis(time, activity)
```

## Parameters
### FitzHugh-Nagumo Parameters
| Parameter | Description | Typical Value |
|-----------|-------------|---------------|
| a         | Time scale of recovery variable | 0.7 |
| b         | Sensitivity of recovery variable | 0.8 |
| c         | Time constant | 12.5 |
| I_ext     | External current | 0.5 |

### Izhikevich Parameters
| Parameter | Description | Typical Value |
|-----------|-------------|---------------|
| a         | Time scale of recovery variable | 0.02 |
| b         | Sensitivity of recovery variable | 0.2 |
| c         | After-spike reset value of v | -65 |
| d         | After-spike reset value of u | 8 |

### Network Parameters
| Parameter | Description | Typical Value |
|-----------|-------------|---------------|
| N         | Number of neurons | 100 |
| p_connect | Connection probability | 0.1 |
| inhibitory_ratio | Fraction of inhibitory neurons | 0.2 |

## Mathematical Background
### FitzHugh-Nagumo Model
The FHN model is a simplification of the Hodgkin-Huxley equations, capturing the essential features of neuronal excitability through:
- Cubic nonlinearity representing fast sodium channels
- Linear recovery term representing slower potassium channels

### Izhikevich Model
The Izhikevich model combines biological plausibility with computational efficiency through:
- Quadratic term for spike generation
- Linear recovery variable
- Reset conditions for spike termination

### Network Dynamics
The network implementation uses:
- Directed graph representation of connections
- Excitatory and inhibitory synapses
- Population-level dynamics analysis

## References
1. FitzHugh, R. (1961). Impulses and physiological states in theoretical models of nerve membrane. Biophysical Journal.
2. Izhikevich, E. M. (2003). Simple model of spiking neurons. IEEE Transactions on Neural Networks.
3. Ermentrout, G. B., & Terman, D. H. (2010). Mathematical foundations of neuroscience.
4. Dayan, P., & Abbott, L. F. (2001). Theoretical neuroscience.

## License
This project is licensed under the MIT License - see the LICENSE file for details.
