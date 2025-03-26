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
