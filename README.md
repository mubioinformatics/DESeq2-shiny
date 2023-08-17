## Guide to Run DESeq2-shiny Container on a Cluster

Please follow the below steps to run the DESeq2-shiny container on a cluster:

1. Remotely access any login node's terminal using the following command:
   ```
   ssh ${USER}@lewis.rnet.missouri.edu

   ssh ${USER}@lewis42.rnet.missouri.edu

   ssh ${USER}@lewis4-dtn.rnet.missouri.edu
   
   ssh ${USER}@lewis4-dtn1.rnet.missouri.edu
   ```

2. Copy the DESeq2-shiny.job file to your home directory using the below command:
   ```
   cp /storage/hpc/group/ircf/software/singularity_DESeq2-shiny/DESeq2-shiny.job ~/DESeq2-shiny.job
   ```

3. Navigate to your home directory using the following command:
   ```
   cd
   ```

4. Check for an available node using the below command:
   ```
   sinfo --state=idle
   ```

5. Modify the "DESeq2-shiny.job" file as per your requirements based on Partition, Node, Memory, MYDATA, etc.:
   ```
   #!/bin/bash
   ##SBATCH -p r630-hpc3
   ##SBATCH -w lewis4-r630-hpc3-node548
   #SBATCH -p Gpu
   #SBATCH -t 0-02:00  # time (days-hours:minutes)
   #SBATCH --ntasks-per-node=10
   #SBATCH --mem=100G
   #SBATCH --output=/home/%u/log_DESeq2-shiny.job.%j
   ##SBATCH --mail-user=youremail@missouri.edu  # email address for notifications
   ##SBATCH --mail-type=END,FAIL  # which type of notifications to send
   #SBATCH -J DESeq2-shiny
   ##SBATCH --account ircf 
   ```

6. Submit the job to the SLURM scheduler using the below command:
   ```
   sbatch DESeq2-shiny.job
   ```

7. Check the job log for instructions by running the below command:
   ```
   cat log_DESeq2-shiny.job.*
   ```