### Analyze Network Features

1. Functional modules can be suggested by highly-connected network regions with similar responses to experimental conditions. These patterns can be detected visually, but in practice the high level of connectivity in interaction networks makes visual detection difficult. Putative modules can be identified with the jActiveModules plugin as follows. Further details are available in the original publication.
  1. Critical Step: Under the **Plugins** menu select **jActiveModules**. This will bring up a jActiveModules section on the Control Panel, listing the available expression experiments.
  
  1. Critical Step: Select all of your expression experiments by clicking on them with the left mouse button (One can run **jActiveModules** on only one expression experiment, or on a subset of the experiments).
  
  1. In the **General Parameters** panel, keep the default values, as these are effective for most initial analyses.
  
    1. **Number of Paths** indicates the number of putative modules that will be reported.
    
    1. **Adjust score for size** corrects for the fact that a larger putative module is more likely to contain nodes with significant p-values by random chance.
    
    1. **Regional scoring** affects how the score of a given module is calculated. Instead of scoring only those nodes within the module, the neighboring nodes of the module are also included. This aids in the identification of active modules in networks that contain nodes with many neighbors (i.e., hubs). Consider a transcription factor with many targets: even if the transcription factor is not active, it is likely that some of it targets will be expressed simply due to random chance.  Without regional scoring, this subset of targets can be selected as an active module, even though this arrangement is not unexpected. In this situation, regional scoring prevents this problem by forcing all targets to be scored simultaneously. 

  1. In the **Strategy** panel, the user can select the search strategy used to identify high-scoring modules.
  
    1. **Search** - In this strategy, local, greedy searches are initiated from single nodes in the network.
    
      1. **Search Depth** - At each step in the greedy search, this parameter determines how close (as determined by shortest path) a node must be to the current active module to be considered for inclusion in the active module.
      
      1. **Max Depth** - This parameter determines how close a node must be to the initial seed node to be considered for inclusion in the active module.
      
      1. **Search from Selected Nodes** - By default, a separate search is initiated for each node in the network. Using this option, searches are only initiated from those nodes selected by the user.
      
    1. **Anneal** - In this strategy, all active modules in the network are discovered simultaneously. Nodes in the network can be turned "on" or "off." A connected set of "on" nodes form an active module. To avoid local optima, a simulated annealing approach is used to guide the global search. As opposed to the local greedy search, this algorithm is stochastic.
    
      1. **Annealing Parameters** - These parameters define the simulated annealing schedule. Over the specified number of iterations, the temperature will be decreased from the **starting temperature** to the **ending temperature**.  In a simulated annealing schedule, the temperature determines the likelihood of accepting low scoring modifications to the current solution.
      
      1. **Annealing Extensions** - These are slight modifications to the simulated annealing search procedure.
      
        1. **Quenching** - After the simulated annealing run is complete, a greedy search will be initiated from the final solution to ensure that a local optima has been reached.
        
        1. **Hubfinding** - In the simulated annealing algorithm, the presence of hubs often confuses the search process. Specifically, it is often difficult to turn hubs "on," as this tends to result in the creation of large, poor scoring modules. With "hubfinding," the nodes surrounding a hub can be turned "off" when that hub is turned "on," preventing the formation of these very large clusters. This improves the detection of high scoring active modules.
        
      1. **Seed Graph Options** - This determines the initial state of the simulated annealing search. By fixing the value of the random seed, the results of the algorithm become deterministic.
      
  1. Critical Step: Click the **Find Modules** button.
  
  1. Shortly, the **Results** panel will appear, as illustrated in Figure 5. This window contains a table in which each row represents one putative module, listed according to the number of nodes, and an associated z-score. Z-scores greater than 3.0 are generally considered significant. The table contains one column per expression experiment; for these columns, any row in which the cell is filled indicates a pathway that showed a significant response under the conditions of the experiment. Clicking on any row causes the corresponding nodes to be selected in the Cytoscape canvas. To view these nodes as a separate network, click on the **Create Network** button. Layout this new network using **Layout → yFiles → Organic** from within the new view.
  
  1. Repeat the Find Modules step a few times. Depending on the settings of the parameters, jActiveModules is based on a Monte Carlo algorithm which relies on random sampling and is not guaranteed to return the same result with each execution. Consequently, it is worthwhile to run jActiveModules repeatedly to ensure that the approach is converging, i.e., the identified modules are reproducible across runs.
  
  1. One method for validating module predictions is to determine if the nodes in the putative module are enriched for any GO biological processes. See Step 26.
