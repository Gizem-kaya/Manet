# Manet
## Mobile Ad-Hoc Network (MANET) Simulator

![0](https://user-images.githubusercontent.com/32525636/82225550-046cb580-992e-11ea-8a8c-651edb322fa1.png)

An implementation a program that simulates MANET. In this project we call simulator as AdHocSim. It is first established the network then found possible routes between sender and receiver nodes finally chosee optimal route among them. To accomplish this task we use recursion while constructing the possible routes.

> MANET comprises of nodes that communicate each other directly or indirectly by employing other nodes as routers in the case of they are not located within the communication range. In this assignment, a node carries three different information: 
1. location, 
2. transmission range,
3. residual battery level. For example, node A is located at (120,45) and has 80% battery level (see Fig. 1).

![1](https://user-images.githubusercontent.com/32525636/82225053-4f39fd80-992d-11ea-8d4f-aef5280b5910.png)

> In order to determine neighborhood of each node, it is first needed to examine the location and transmission range information. To say
A is one of the neighbors of B, A should be within the transmission range of B. As mentioned, every node has location and transmission
range information which is determined by east (x1), west (x2), north (y1), and south (y2) coordinate limits. For example B and C are the two neighbors of A (see Fig. 2). 

Note: To represent neighborhood we  construct a dictionary where key is node label and its corresponding value is its neighbors, as illustrated follows. There is an example of dictionary that stores relations:

'A': ['B', 'C']
'B': ['D', 'E']
'C': ['F', 'H']
'D': ['E', 'G']
'E': ['G']
'F': ['G', 'H']
'G': ['I']
'H': []
'I': []
