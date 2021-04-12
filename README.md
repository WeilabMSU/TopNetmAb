# Machine learning model for binding free energy (BFE) change predictions
This code is for BFE change predictions of monoclonal antibodies binding to SARS-CoV-2 Spike protein. The zip file can be download from `https://weilab.math.msu.edu/TopNetmAb.tar.gz`
******
## File description
There are five folders after extracted. 
* **bin**
    * jackal.dir
    * jackal_64bit
    * mibpb5
    * MS_Intersection
    * PPIprepare
    * PPIstructure
    * profix
    * scap
    * **SPIDER2_local**
* **7NDB**
    * **features**
        * **7NDB_B_A_344_S**
            * 7NDB.pdb
* **dataset**
    * 6M0J_ACE2.txt [1]
    * 6M0J_RDB1.txt [2]
    * 6M0J_RBD2.txt [3]
    * 7KL9_CTC640.txt [3]
    * 7KL9_RBD.txt [3]
    * skempi2_list.txt [4]
* **models**
    * ANN_model.pkl (trained ANN machine learning model)
    * normalizer.pkl (normalizer for ANN machine learning model)
    * GBDT_model.pkl
* **predicting**
    * 7NBD_B_A_344_S.npy
    * prediction_ANN
    * prediction_GBDT.py

**Important!!!** The program `PPIprepare` and `PPIstructure` will copy the file from `"../../../bin/"`. Thus, the folder path, such as `7NDB/features/7NDB_B_A_344_S` shouldn't be changed and users should run `PPIprepare` and `PPIfeature` under the folder `7NDB/features/7NDB_B_A_344_S/`.

## Feature generation
There are two executable files for the feature generation, which are `PPIprepare` and `PPIfeature`.  The dependencies libraries (the current version is only test on linux system):

* BLAST+/2.10.1
* dssp/3.1.4
* vmd (should be a global call)
* pdb2pqr (should be a global call)
* mibpb5 (should be a globale call, which is in the folder `bin`)

Except `mibpb5`, users should install the rest libraries.
`mibpb5` is included in the folder `bin`.

A PDB file is required when run the program. When run `PPIprepare` and `PPIfeature`, users should know: 

* PDBid: 7NDB
* Antibody chain ID: HL
* Antigen chain ID: B
* Chain ID with target mutation: B
* Residue wild type: A
* Residue ID: 344
* Residue mutant: S
* Ph value: 7.0

Now, users can generate the feature as:

`PPIprepare 7NDB HL B B A 344 S 7.0`

`PPIfeature 7NDB HL B B A 344 S 7.0`

A file named `7NDB_B_A_344_S.npy` stores the features for 7NDB_B_A_344_S.

## Predicting
In `predicting` folder, there are three files, where `7NDB_B_A_344_S.npy` is the features of PDB 7NDB with a mutation on Chain B, A344S, `prediction_ANN` and `prediction_GBDT.py` are prediction files.
`prediction_ANN` is an executable file which requires a GPU integrated system. `prediction_GBDT.py` can be run on any system.

To run `prediction_ANN`:

`$ ./prediction_ANN --predict_data 7NDB_B_A_344_S.npy`

By copying and pasting features to the fold `predicting`, users can predict BFE changes for other complexes and mutations.

To run `prediction_GBDT.py`:

`$ python prediction_GBDT.py`
## Datasets
Six datasets are presented in this folder. The following list includes the corresponding references.
1. Kui K Chan, Danielle Dorosky, Preeti Sharma, Shawn A Abbasi, John M Dye, David M Kranz, Andrew S Herbert, and Erik Procko. Engineering human ACE2 to optimize binding to the spike protein of SARS coronavirus 2. *Science*, 369(6508): 1261–1265, 2020.

1. Tyler N Starr, Allison J Greaney, Sarah K Hilton, Daniel Ellis, Katharine HD Crawford, Adam S Dingens, Mary Jane Navarro, John E Bowen, M Alejandra Tortorici, Alexandra C Walls, et al. Deep mutational scanning of SARS-CoV-2 receptor binding domain reveals constraints on folding and ACE2 binding. *Cell*, 182(5):1295–1310, 2020.

1. Thomas W Linsky, Renan Vergara, Nuria Codina, Jorgen W Nelson, Matthew J Walker, Wen Su, Christopher O Barnes, Tien-Ying Hsiang, Katharina Esser-Nobis, Kevin Yu, et al. De novo design of potent and resilient hACE2 decoys to neutralize SARS-CoV-2. *Science*, 370(6521):1208–1214, 2020.

1. Justina Jankauskaitė, Brian Jiménez-Garcı́a, Justas Dapkūnas, Juan Fernández-Recio, and Iain H Moal.
Skempi 2.0: an updated benchmark of changes in protein–protein binding energy, kinetics and thermo-
dynamics upon mutation. Bioinformatics, 35(3):462–469, 2019.
