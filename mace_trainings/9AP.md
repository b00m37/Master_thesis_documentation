I tried training MACE potentials on my 9AP data

On Cineca, I trained some potentials in the following folder:
/leonardo_scratch/fast/IscrB_LiCaDec/Sebastian/9AP

First, I only trained on data from the S enantiomer

## only_s_2L

Training on S enantiomer, using num_channels=128 and max_L=2. The minimum on validation error was reached pretty early, after which
the validation error kept rising.


## only_s_2L_short

Since the minimum for the validation error is reached so early, I tried using early stopping with the --patience argument. However, it didn't output a model that is straightforward to use.

Then, I trained some models on both both s and r enantiomers