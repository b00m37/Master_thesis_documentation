This is an overview of all my attempts to train potentials.

# On the initial training set
## model1
First attempt at training a model

## model2 and model3
Like model 1, with different seeds. By mistake, I did not change all seeds in the input file

## model4 and model5
I changed all seeds in the input file. Results presented in my semester project were computed with models 1, 4 and 5.

## model6, model7 and model8
I noticed a mistake in the training set regarding the atom types in the R configurations. In models 6,7 and 8, I corrected that mistake.

## model9, model10, model11 and model12
I increased the training time, which improved training loss convergence slightly.

## model13
I introduced a train-validation split and increased the training time further

## model14
I made the learning rate decay less drastically. This worked better than model13 in terms of training and validation error.

## model15
Even larger learning rate compared to model14. Worked worse than model14 in terms of training and validation error.

## model16, model17 and model18
Like model14, with different seeds.

## model19
Much smaller fitting net.

## model20
small fitting net (like model19), short training (like model1)

## model21
Trained only on bulk and slab of PdGa (Not molecule)

## model22
Also only PdGa bulk and slab, but longer training than 21

## model23
Bigger value for stop_lr

## model24 and model25
Identical to model22, but with different seeds

## model26
Bulk only (no slab), short training

## model27
Like 26, but removed unneeded atom types from type_map in input.json (I don't think this changes much)

## model28
Only slab (fixed and unfixed opt, no bulk), short training.
-> Still very high training error

## model29
Only slab_fixed_opt -> still high training error

## model30
Trained on a very small set (4 configs) of bulk configurations. Those 4 configs have all normed forces smaller than 4 eV/A per atom. Still high training RMSE.

## model31
Like 30, but smaller network. Still high training RMSE.

## model32
Trained on the set bulk_outliers_removed, and a small network. That set contains only about 100 configurations, with forces smaller than 4 eV/A per atom.

## model33
Only slab_unfixed_opt

## model34
Only one configuration, which is the starting configuration of the bulk dynamics (before any dynamics had taken place). This means that this model is independent on NN-MD.

## model35
Trained from bulk AIMD configurations. During AIMD, a small convergence threshold was chosen and forces were printed directly during dynamics. (It turns out I matched forces and configurations wrong in this run)

## model36
Only 40 last configurations from bulk AIMD

## model37
Ran single points on some of the bulk AIMD configurations and tried training on them

## model38
Like 37, but smaller network

## model39
Also small network, but se_e3 descriptor

## model40
Trained only from bulk AIMD configurations. The matching between forces and configurations should be correct now.


