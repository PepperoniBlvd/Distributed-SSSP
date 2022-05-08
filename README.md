# Distibuted-SSSP
## About the project

I created this project to dive deep into Distributed Systems programming and go beyond what I learn in class. This project demonstrates the implementation of serial, parallel and distributed version of Dijkstra's algorithm to solve **Single Source Shortest Path** problem for directed unweighted graph.

## To generate input graphs

1. Create a file called `testGraph.txt` , with the list of edges (one edge on each line in "`<source> <destination>`" form) in the graph. For example,

   ```cpp
   1 2
   2 3
   ```

2. Run `input_graphs/SNAPtoBinary testGraph.txt testGraphConverted`. This will create `testGraphConverted.csr` and `testGraphConverted.csc` files which are [CSR and CSC](https://en.wikipedia.org/wiki/Sparse_matrix#Compressed_sparse_row_(CSR,_CRS_or_Yale_format)) representations of the graph.

3. To use the graphs in your solutions, use the command line argument `--inputFile "testGraphConverted"`.

4. Note that you can also convert any large graphs form the Stanford repository (https://snap.stanford.edu/data/index.html) by downloading the graph file then using the same SNAPtoBinary script above. 


## Compile

1. To compile all the code, use the following command.

   ```shell
   make
   ```

2. To compile the serial implementation, use the following command.

   ```shell
   make SSSP_serial
   ```

3. To compile the parallel implementation, use the following command.

   ```shell
   make SSSP_parallel
   ```

4. To compile the distributed implementation, use the following command.

   ```shell
   make SSSP_MPI
   ```

## To run the serial implementation

1. To run the executable of the serial implementation, use the following command.

   ```shell
   ./SSSP_serial --sourceVertex 1 --inputFile absolute_path_of_input_graph --y_or_n yes
   ```

   `--sourceVertex`: the ID of the source vertex

   `--inputeFile`: absolute path of the input graph

   `--y_or_n`: whether or not to print out the shortest path

2. Run the executable file SSSP_serial on Slurm cluster:
   create a a bash script  in the following format:

   ```shell
   #!/bin/bash
   #
   #SBATCH --cpus-per-task=1
   #SBATCH --time=05:00
   #SBATCH --mem=10G
   #SBATCH --partition=fast
   
   srun ./SSSP_serial --sourceVertex 1 --inputFile absolute_path_of_input_graph --y_or_n yes
   ```

   run it on Slurm by command:

   ```shell
   sbatch filename.sh
   ```

## To run the parallel implementation

1. To run the executable of the parallel implementation, use the following command.

   ```shell
   ./SSSP_parallel --nThreads 4 --sourceVertex 1 --inputFile [absolute_path_of_input_graph] --displayOutput [yes/no]
   ```

   `--nThreads`: number of threads

   `--sourceVertex`: the ID of the source vertex

   `--inputFile`: the absolute path of the input graph

   `--displayOutput`: whether to print out the result of the shortest path

2. Run the executable file SSSP_parallel on Slurm cluster:
   create a a bash script  in the following format:

   ```bash
   #!/bin/bash
   #
   #SBATCH --cpus-per-task=4
   #SBATCH --time=05:00
   #SBATCH --mem=10G
   #SBATCH --partition=fast
   
   srun ./SSSP_parallel --nThreads 4 --sourceVertex 1 --inputFile [absolute_path_of_input_graph] --displayOutput [yes/no]
   ```

   run it on Slurm by command:

   ```bash
   sbatch filename.sh
   ```

## To run the distributed implementation

1. Run the executable file SSSP_MPI locally:

​		type the following command in terminal:

```shell
mpirun -n num_processes ./SSSP_MPI --sourceVertex vertex_num --inputFile path_of_graph --y_or_n str 
```

​	Arguments:

​	`--num_precesses`: indicates the number of processes used   

​	`--sourceVertex`: indicates the vertex number of the source vertex

​	`--inputFile`: indicates the path of the input graph 

​	`--y_or_n`: can only be "yes" or "no". "yes" indicates printing out the detailed result, "no" indicates otherwise.

​	sample command:

```shell
mpirun -n 4 ./SSSP_MPI --sourceVertex 0 --inputFile input_graphs/testG1 --y_or_n yes
```

2. Run the executable file SSSP_MPI on Slurm cluster:
   create a a bash script  in the following format:

```shell
#!/bin/bash
#
#SBATCH --cpus-per-task=1
#SBATCH --nodes=1
#SBATCH --ntasks=4
#SBATCH --partition=fast
#SBATCH --mem=10G

srun ./SSSP_MPI --sourceVertex 0 --inputFile input_graphs/testG1 --y_or_n yes
```

​	options:
​	`--ntasks`: indicates the number of processes used

​	run it on Slurm by command:

```shell
sbatch filename.sh
```

