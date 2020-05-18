# Manet
## Mobile Ad-Hoc Network (MANET) Simulator

![0](https://user-images.githubusercontent.com/32525636/82229420-156bf580-9933-11ea-86e2-a044fb9a0bf9.png)

> An implementation a program that simulates MANET. In this project we call simulator as AdHocSim. It is first established the network then found possible routes between sender and receiver nodes finally chosee optimal route among them. To accomplish this task we use recursion while constructing the possible routes.

### Setting-up the Nodes and the Neighbors

  MANET comprises of nodes that communicate each other directly or indirectly by employing other nodes as routers in the case of they are not located within the communication range. In this assignment, a node carries three different information: 
1. location, 
2. transmission range,
3. residual battery level. For example, node A is located at (120,45) and has 80% battery level (see Fig. 1).

![1](https://user-images.githubusercontent.com/32525636/82229426-169d2280-9933-11ea-98e6-1470b7521dc3.png)

  In order to determine neighborhood of each node, it is first needed to examine the location and transmission range information. To say
A is one of the neighbors of B, A should be within the transmission range of B. As mentioned, every node has location and transmission
range information which is determined by east (x1), west (x2), north (y1), and south (y2) coordinate limits. For example B and C are the two neighbors of A (see Fig. 2). 

  Note: To represent neighborhood we  construct a dictionary where key is node label and its corresponding value is its neighbors, as illustrated follows. There is an example of dictionary that stores relations:

>'A': ['B', 'C']
>'B': ['D', 'E']
>'C': ['F', 'H']
>'D': ['E', 'G']
>'E': ['G']
>'F': ['G', 'H']
>'G': ['I']
>'H': []
>'I': []

### Route Finding in MANET

  We may think of a network as a directed graph where nodes represent vertices whereas communication links represent edges. A graph might be cyclic or acyclic. A graph is said to be cyclic if there exists some vertices that are connected in a closed chain (see Fig. 2 for an example of acyclic graph).

![2](https://user-images.githubusercontent.com/32525636/82225203-91fbd580-992d-11ea-8239-1f142b684b3a.png)  

  In this project, it is obtained cyclic or acyclic network once we set-up nodes and their neighbors successfully. Concretely speaking, there might be a case where the next node is a node that has already been visited before. 

  After setting up the nodes and determining of neighbors of every node, we obtain a network ready-to-use. Before transmission of first packet begins, it is needed to find a path through which packets are transferred. This path is called as route that starts and ends with a sender and destination nodes, respectively. Remember that route consists of only sender and destination nodes if they are within each other’s transmission range. But, on the other, they employ other nodes as intermediate nodes by treating them routers for transmission of a collection of packets. 

  To clarify the routing process in MANET, we make use of Fig. 3. From the figure, sender node A is ready to initiate a data transfer to destination node I and there exist four routes between A and I. (Note: There might be cases where there is no route between any given two nodes.) A step by step route finding process is demonstrated with figures at the end of this document. With a similar way, we found every possible routes, using recursion, with its cost whose calculation is explained in the following section.

### Selecting an Optimal Route

  This process is similar to what actually navigation application does. Suppose Alice wants to visit Bob and uses his application to take a route to Bob’s house. Application returns Alice’s request with a route within a series of possible routes, which is often shortest path with respect to the time or distance. In this scenario time and distance are the two costs that determine the quality of the routes. Similar to this scenario, one needs to determine one of the routes to use for packet transmission depending on the their costs after finding all routes. The cost of a route is the sum of the cost of every communication links (L) between nodes (see Eq. 1 and Fig. 4). 
  
* Cost(Router) = XCost(i, j) | i, j ∈ L (1)

  We consider distance and residual battery level for the calculation of cost of a link between nodes i and j given by:


* Cost(i, j) = disti,j/batteryj

  where disti,j is a distance between the nodes i and j. As these nodes are actually represented by two points on the Cartesian plane (ix and iy are two points of node i whereas jx and jy are the two points of node j), we get the distance between them using Euclidean
distance:

* disti,j = srtq((ix − jx)^2 + (iy − jy)^2)

![4](https://user-images.githubusercontent.com/32525636/82229102-a9898d00-9932-11ea-9a25-57c643689397.png)

  In MANETs, apart from initial data transfer, it is also necessary to find routes every time a link breakage occurs. Link breakage problem arises mostly when a node leaves the route through which data packets are transferred. A node becomes unreachable either if it runs out of its battery or goes beyond the transmission range of a node from which it receives packets. That’s why distance and residual battery level has been intentionally included in the calculation of every link cost in this assignment. As the probability of a node being exceeded transmission range gets lowered with a decrease in distance between two nodes, it is rational to select a link having a more closer one. Similarly, a link destined to a node having higher residual battery level should also be selected as it is lower probability of such node being left due to the drainage of battery. Therefore, the optimal route (RouteOPT) selection among possible routes (R) is done as follows:

* RouteOPT = argm r min Cost(Route r) | r ∈ R
