I tried training MACE potentials on my 9AP data

# On Cineca

On Cineca, I trained some potentials in the following folder:
/leonardo_scratch/fast/IscrB_LiCaDec/Sebastian/9AP

First, I only trained on data from the S enantiomer

## only_s_2L

Training on S enantiomer, using num_channels=128 and max_L=2. The minimum on validation error was reached pretty early, after which
the validation error kept rising.


## only_s_2L_short

Since the minimum for the validation error is reached so early, I tried using early stopping with the --patience argument. However, it didn't output a model that is straightforward to use.

Then, I trained some models on both both s and r enantiomers. However, those potentiels worked worse.

I then noticed all models trained on Cineca using the S enantiomer had an error regarding the periodic boundary conditions during training

# On Daint

In the folder /capstor/scratch/cscs/sbrovell/mace/9AP, I also trained some potentials. I noticed an error in the periodic boundary conditions during training and corrected it.

## r_iteration0, s_iteration0

Trained on only R and S enantiomers, respectively.

## s_r_iteration0

On both R and S enantiomer, but it didn't complete properly

## s_r_iteration0_train2

Also both R and S enantiomer, completed.

## s_r_bulk_it0 and s_r_bulk_slab_it0

I tried adding in the bulk and slab configurations, but it made the error worse. Possibly because the bulk and slab configurations used a different cell size or maybe I made another error.

## s_r_gas*

These are some attempts to include gas phase configurations to the training. However, the training didn't finish correctly.

## more_training_with_gas

