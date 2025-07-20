# On Cineca



# On Tigu2

I ran one 

# On Daint

In the directory /capstor/scratch/cscs/sbrovell/mace/lammps/9ap I ran some dynamics with lammps and plumed using mace potentials

## 100K_OPES

short 100K run (about 40 ps) with OPES using barrier=50. No reaction occured.


## 100K_OPES_long

That one didn't even start

## 300K_OPES_debug

Short 300K run with OPES using debug partition. It crashed quickly.

## 300K_OPES_new_model

I corrected a mistake in I made in training regarding the pbc. With the new model, I ran at 300K. In the 10 ps it ran, the simulation didn't explode, but a Gallium atom was ejected from the surface.

## 200K_OPES_new_model_long

Stable for a short time but cancelled due to node failure. Trying again now.
Now it's running properly but a gallium atom leaves the surface. water atom 5 (0 indexing) gets closer and further to C until it flys away.

## 100K_OPES_new_model_long

100K dynamics with same model as before. as the H atoms approached, the molecule exploded.

## 100K_OPES_new_model_long_restart2

I restarted from a previous checkpoint of 100K_OPES_new_model_long to see if I would get a different behaviour. It also exploded.

## 200K_OPES_new_model_extpot_debug

I tried adding an external potential to keep the H on the surface. I chose the same external potential that was also used for the CP2K ab initio dynamics. The temperature exploded in the end and one of the H atoms flew off. I am not sure if the potential is right:\
FUNCTION  0.000000000001*(Z-20/0.52918)^8\
That's because that is a conversion from Bohr to angstrom.

## 200K_OPES_new_model_extpot_debug2

Removed the conversion factor and tried again on a short run. The new potential is defined as 0.000000000001*(Z-20/0.52918)^8.

## 200K_OPES_new_model_extpot

Long run with the external potential 0.000000000001*(Z-20/0.52918)^8 on H atoms. Still, one of the H flew off.

## 200K_OPES_new_model_lj93

Attempt at introducing a lj93 wall. The H-Atoms didn't leave the crystal at all. After that were a few attempts at making it work, which I'm not gonna list all of them. The reason was that I needed to apply the fixes in the right order.

## debug_lj93_different_order

Here, I put the fixes in the right order, and the H atoms were able to leave the crystal. However, they flew into the minimum uf the lj93 potential and got stuck at around z=25.

## 200K_ramp_lj93 and 200K_restart_from_ramp_lj93

I slowly increased the temperature from 10K to 200K (first folder) and then let it run from 200K (second folder). The H atoms still got stuck in the minimum. OPES was already active during the 

## 200K_ramp_unbiased

Slow increase from 10K to 200K with OPES inactive.



## testing_walls

In this folder, I tested multiple different walls, always restarting from 200K_ramp_unbiased

### testing_walls/200K_lj93

Using lower wall (z=24) with an lj93 potential

TODO

# On Daint: 9ap/starting_from_products

In the folder /capstor/scratch/cscs/sbrovell/mace/lammps/9ap_with_gas, I did some runs starting from the fully hydrogenated product of the S enantiomer and with no other free H atoms present.

## run4
Coordination numbers different; only from one C/O atom to one H atom. O dehydrogenated, but not C. 100K.

## run5
Like run4, but different parameters for CVs. Both dehydrogenated. 100K.

## with_gas
CVs like run5, but with new model that includes gas phase configurations (trim6) and 200K. First O dehydrogenated, then after a while C and then it crashed.

## with_gas_other_cv
Like with_gas, but including distance in CVs. It crashed quickly.




# On Daint: 9ap_with_gas

In the folder /capstor/scratch/cscs/sbrovell/mace/lammps/9ap_with_gas, I did some dynamics with models that were trained by including gas phase configurations. test1 and test2 were done with potentials that didn't converge properly during training.

## test3

200K OPES dynamics with the model from /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim6/. O hydrogenated quickly, but it exploded before the second hydrogenation.

## test_ramp
An unbiased, slow increase from 10 to 200K, using the model of /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim4.

## 200K_unbiased_from_ramp_trim6
Unbiased dynamics, restarting from test_ramp, using the model of /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim6. Not much happened.

## 200K_introducing_bias_trim6

Restarting with OPES from 200K_unbiased_from_ramp_trim6, using the trim6 model. An H got close to O, but it exploded before the hydrogenation occurred.

## 200K_from_ramp_trim4
Restarting from test_ramp, using the model of /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim4. Oxygen hydrogenated, but the molecule exploded before the second hydrogenation. Slab remained stable.

## 200K_from_ramp_trim6
Restarting from test_ramp, using the model of /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim6. Oxygen hydrogenated, but the slab and molecule exploded before the second hydrogenation

## 300K_from_ramp_trim6
Restarting at 300K from test_ramp. It exploded quickly.


## 200K_from_ramp_trim6_256

Restarting from the trajectory in test_ramp, I did some OPES dynamics using the model from /capstor/scratch/cscs/sbrovell/mace/9AP/more_trainings_with_gas/E0s_set_trim6_256. THis model uses --num_channels=256. It exploded because some Gallium atoms contracted. Possibly due to the interaction between Hydrogen and Gallium.

## 200K_5_moved

In most of these simulations from 9ap_with_gas, O hydrogenated first with H atom 5 (0-indexing), because it is close. I moved that atom to another place to see what would happen. The molecule moved around, but it crashed.

## 300K_unbiased_from_ramp_trim6

Restarting from test_ramp, I did a 300K unbiased dynamics using the trim6 model. It seems stable so far.

## 200K_no_gas_E0s_set_trim6
I trained a new model in /capstor/scratch/cscs/sbrovell/mace/9AP/s_r_without_gas_E0s_set_trim6, whith computed E0s but without gas phase configurations. Here, I did a dynamic with that model but it crashed (Some molecules in the slab also moved).

## 200K_no_gas_E0s_set_trim6_2
Same as 200K_no_gas_E0s_set_trim6, but different in lammps. Still going.

# On Daint: 9ap_more_H

In the foder /capstor/scratch/cscs/sbrovell/mace/lammps/9ap_more_H, I added more hydrogen atoms to the slab and did dynamics with H in all of the palladium trimers.

## test1

First test. In the beginning, one H atom was pushed away, but then the 9AP molecule approached some other H atoms. The slab exploded after a while (Gallium atoms moved)

## test2

Exactly as test1, but with different seed. The molecule exploded, but the slab remained stable.

