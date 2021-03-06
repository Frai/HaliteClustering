Halite - basic information

Halite is an algorithm (and a library) for scalable clustering of high-dimensional data. For more information, see the paper "Halite: Fast and Scalable Multiresolution Local-Correlation Clustering" by Robson L. F. Cordeiro, Agma J. M. Traina, Christos Faloutsos and Caetano Traina Jr.

Included is the C++ API for the algorithm (haliteClustering.cpp), as well as a demo program (Halite.cpp). 

If you want to use the code, the easiest way would just be copying the source files into your project, as it's not set up to build or install a library.

*******************************************************************

input data format:
 
axis_1 axis_2 axis_3 ... axis_d groundTruthCluster
axis_1 axis_2 axis_3 ... axis_d groundTruthCluster
				.
				.
				.
axis_1 axis_2 axis_3 ... axis_d groundTruthCluster				

Example: databases\12.dat

Obs.: - the groundTruthCluster data is not used by Halite.
      - the file databases\12d.sub contains the ground truth WRT the clusters' subspaces for our example dataset, but it's also not used by Halite.
      - you may use this ground truth information to evaluate the quality of Halite's results on our example dataset.

*******************************************************************

output data format: 

ClusterResult1 relevanceOfAxis_1 relevanceOfAxis_2 ... relevanceOfAxis_d
ClusterResult2 relevanceOfAxis_1 relevanceOfAxis_2 ... relevanceOfAxis_d
				.
				.
				.
ClusterResultk relevanceOfAxis_1 relevanceOfAxis_2 ... relevanceOfAxis_d
LABELING
PointId clusterId
PointId clusterId
	.
	.
	.
PointId clusterId

Obs.: - relevanceOfAxis_j = 0 means that axis j is irrelevant to the corresponding cluster, while relevanceOfAxis_j = 1 means that axis j is relevant to this cluster.
      - PointId identifies one point by referring to the line in which this point is found in the input data file. For soft clustering, each PointId value can be related to more than one clusterId value.
      - clusterId = 0 means that the corresponding point is an outlier.

Example: results\result12d.dat

*******************************************************************
compiling Halite:

First, you must install two third-part software:
   - Oracle Berkeley DB: "http://www.oracle.com/technetwork/database/berkeleydb/overview/index.html"
   - OpenCV: "http://opencv.willowgarage.com/"

Then, compile the code using any standard c++ compiler using make.

*******************************************************************

running Halite:

Halite \alpha H hardClustering initialLevel dim memoryMode

Obs.: - the input/output specs are defined in "arboretum/ioSpecs.h".
      - the default value for \alpha is 1e-10.
      - the default value for H is 4.
      - hardClustering = 1 means that the result will be a dataset partition (one point belongs to at most one cluster).
      - hardClustering = 0 means that the algorithm will do soft-clustering (one point can belong to more than one cluster).
      - the default value for initialLevel is 1.
      - dim specifies the dimension of the input data.  The demo provided has dimension 12 data
      - distinct forms of memory management are possible by changing the memoryMode parameter. "memory==0" means that both the dataset and the tree will be put in main memory. "memory==1" means that only the tree will be put in main memory. "memory==2" means that only the dataset will be put in main memory. "memory==3" means that neither the database nor the tree will be put in main memory.

Example: make demo (Linux or Mac OS), runExample.bat (Windows).
