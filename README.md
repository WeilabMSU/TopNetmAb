# Machine learning model for binding free energy (BFE) change predictions
This code is for BFE change predictions.
******
## File description
There are two folder after extracted. 
* `bin`
    * jackal.dir
    * jackal_64bit
    * mibpb5
    * MS_Intersection
    * PPIprepare
    * PPIstructure
    * profix
    * scap
    * `SPIDER2_local`
* `7NDB`
    * `features`
        * `7NDB_B_A_344_S`
            * 7NDB.pdb
* `dataset`
    * 
* `models`
    * ANN_model.pkl (trained ANN machine learning model)
    * normalizer.pkl (normalizer for ANN machine learning model)
    * GBDT_model.pkl
* `training`

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


## Datasets
