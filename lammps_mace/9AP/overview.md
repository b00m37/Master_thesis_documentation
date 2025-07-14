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

# On Daint: 9ap_with_gas

