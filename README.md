# Dynamic Traffic Management with Qutrits

We are **Team QPower** and this project was made as part of IBM's Technical challenge at QC Hack 2021.

## Project Idea

The implementation that we conceptualized for the use of three distinct energy states in a Quantum Computer was the use of variational hybrid algorithms to optimize traffic grids. While it was at first quite challenging to think of a real-world use for three orthogonal basis states (the |0>, |1>, and |2> states), we eventually came to the conclusion that four-way intersections behave with three distinct settings that can be generalized as nodes in quantum systems, affecting the energy of the system like the settings of traffic lights affect the congestion in the grid.   

Unlike what one might initially think, these three states are *not simply Green, Yellow, Red*: this system doesn’t translate to the quantum paradigm as yellow is not truly orthogonal from red, it is simply a precursor. Instead, we have defined the **|0>, |1>, and |2> states** of an intersection to be 
1. Green lights allowing North/South traffic to pass
2. Green lights allowing East/West traffic to pass
3. Red lights allowing pedestrians to cross

This paradigm does take into account two-directional traffic, but does not bother with components of reality that don’t quite affect the math (e.g. yellow lights, protected left turns, etc.).

## Implementation Details

### Data Structure to model traffic intersections
We implemented a custom data structure in Python that would allow the user to create an **n-by-m grid** of nodes (intersections), and to declare which segments of road between the nodes are being used as roads. To better map this situation to a traditional graph-based combinatorial optimization problem, the user can also add “weights” to each edge in the graph, which we conceptualized as some function of the cars held up on that street times the amount of time they have been waiting.  

### Cost Function 
We then designed a rather complex cost function based on a number of assumptions (e.g. the probability of turning left/right at any given light) in order to determine for a given bitstring of assignments for the stoplights (between 0, 1, and 2) and a given list of congestion weights for time t, what the congestion along each edge will probabilistically be at time t + 1. This was, of course, very challenging and tedious, and thus we are left with several areas of improvement on this function.  

**Scope of improvement:** One notable area for improvement is the lack of consideration for pedestrians’ separate weight factor on each edge (as they wait for opportunities to cross), as pedestrians are free to travel in the |2> state while vehicles are not. This would make the |2> state much more likely to appear in the optimal allocation of states. After this, we constructed a simple p-layer implementation of **Farhi’s QAOA** on this unique data type to find the optimal setting of any given traffic grid’s lights in order to minimize pressure and congestion.


## Future Work 
Due to time constraints and limited understanding of Qiskit’s ability for higher-energy value inclusion in quantum computation (as well as the general uncertainty of using the |2> state reliably in any quantum computation), we were not able to fully implement a discretion and classification system for the simulation to discriminate between three possible basis states upon measuring the system, and that would certainly be a priority improvement given more time and resources.  

However, the main component and feat of this project is the idea of a very useful application for large-scale quantum computing. Currently, traffic grids around the world are terribly inefficient, running on timers and excessively general models, as they are incapable of doing a real-time combinatorial optimization problem at the speed of a quantum computer. For a grid with n nodes, it would take a classical computer O(3n) to optimize over all possible combinations—with QAOA, we see a dramatic speed-up. While we might have been unable to implement IBM’s pulse functions to set up discrimination between excited states, we were certainly able to sketch a rough diagram of an interesting and valuable application.


## About the team

1. Syed Farhan Ahmad
2. Shaun Radgowski
3. Chad
4. Anush Krishna
5. Mohamed Yassine