# The training data
First, Ray used data from ab initio molecular dynamics/metadynamics. Then, he ran some trajectories using the first deepmd potential and did one cycle of active learning.
The data from AIMD had the error, that, during single point calculations, some atoms were fixed, resulting in 0 forces. Thus, I had to recompute them. The data from the first
cycle of active learning did not have that error, and I did not have to recompute it.

This was the training used in Ray's final potential:

                        "/scratch/project_465000480/amadorra/data_dbba_mtd/angle_M_MC_small_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/angle_C_AC_small_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/small_M_AM_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/small_A_AC_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/angle_A_AC_small_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/angle_M_AM_small_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/small_M_MC_600K",
                        "/scratch/project_465000480/amadorra/data_dbba_mtd/small_C_AC_600K",

                        "/scratch/project_465000480/amadorra/a1_seed1/singlepoints/int1",
                        "/scratch/project_465000480/amadorra/a1_seed1/singlepoints/int2",
                        "/scratch/project_465000480/amadorra/a1_seed1/singlepoints/int3",

                        "/scratch/project_465000480/amadorra/c1_seed1/singlepoints/int1",
                        "/scratch/project_465000480/amadorra/c1_seed1/singlepoints/int2",
                        "/scratch/project_465000480/amadorra/c1_seed1/singlepoints/int3"
The first 8 folders are from ab initio metadynamics. The others are from active learning.
## Data from AIMD
In the folder /capstor/scratch/cscs/sbrovell/recompute_dbba, I recomputed single points without fixed atoms. At first, I only recomputed on a small subset, but then I recomputed the entire
training set. folder starting with full_recompute_* contain the full single point calculations without fixed fatoms. I then converted everything into extended xyz files for mace.

## Data from neural Nntwork dynamics (active learning)
The data from neural networks dynamics did not need to be recomputed. I copied the data into /capstor/scratch/cscs/sbrovell/correct_dbba and converted it into extended xyz files using my script make_extended_xyz.py to convert the numpy files (used for deepmd) into extended xyz files (used for mace). NOTE: Ray did not use the slab configurations (from active learning), but I did. Not sure if it makes a difference.

## Folder containing all the data
I then collected all the data mentioned above into the following folder:
    /capstor/scratch/cscs/sbrovell/mace/data_dbba_correct
Individual training sets are contained in
    /capstor/scratch/cscs/sbrovell/mace/data_dbba_correct/individual_sets

train_a1.xyz, train_c1.xyz and train_slab1.xyz are from active learning, the rest is from ab initio.

## Adding new data
To add new training data, add new .xyz files into the folder "individual_sets". Then, create a new total training file, containing all the training data like this:
    cat individual_sets/train* > train_new.xyz

# Training

The first trained model is found here

    /capstor/scratch/cscs/sbrovell/mace/dbba_correct/train2/swa/dbba_compiled.model-lammps.pt
To train a new model, you can modify the script in
    
    /capstor/scratch/cscs/sbrovell/mace/dbba_correct/train2/train.sh

After training, the final model will be in a folder called "swa".

IMPORTANT

In mace, you can give more weight to some types of configurations. This might be important, if you only have 25 gas phase configurations.
Currently there are thes types of configurations:
* dbba_it0 (ab initio data)
* dbba_c1_1 (active learning data on c enantiomer)
* dbba_a1_1 (active learning data on s enentiomer)
* dbba_slab_1 (active learning data on slab)
To add more weight to the gas phase configurations, add an argument to fixed_args in train.sh. For example, if you called your gas configurations "dbba_gas_phase", you could use this for example:
    
    --config_type_weights '{"dbba_it0": 1.0, "dbba_c1_1": 1.0, "dbba_a1_1": 1.0, "dbba_slab_1": 1.0, "dbba_gas_phase": 10.0}'

Also, since there is more active learning data than AIMD data, you may also give more weight to dbba_it0. (You can check the size of the sets in /capstor/scratch/cscs/sbrovell/mace/data_dbba_correct/individual_sets)


## Length of training
I use a pretty short training, since the validation error stops improving after only a few epochs. If you check the logs and find that the validation error is still decreasing in the end, you may do a longer training. (more wall time, increase BOTH cases of  max_num_epochs). But if the validation error has already stopped improving, there is no point in a longer training.