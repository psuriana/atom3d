# ATOM3D: Tasks On Molecules in 3 Dimensions

[![Documentation
Status](https://readthedocs.org/projects/atom3d/badge/?version=latest)](http://atom3d.readthedocs.io/?badge=latest)

ATOM3D enables machine learning on three dimensional molecular structure.

## Features

* Access to several datasets involving 3D molecular structure. 
* Sharded data format for storing lots of molecules (and associated metadata).
* Utilities for splitting/filtering data based on many criteria.

## Installation

Install with:

```
pip install -r requirements.txt
```
    
To use rdkit functionality, please install within conda:

```
conda create -n atom3d python=3.6 pip rdkit
conda activate atom3d
pip install -r requirements.txt
```

## Usage

### LMDB datasets.

LMDB allows for compressed, fast, random access to your structures, all within a
single database.  Currently, we support creating LMDB datasets from PDB files
and silent files.

#### Creating an LMDB dataset using PDB files.

From command line:
```
python atom3d/torch/dataset.py PATH_TO_PDB_DIR PATH_TO_LMDB_OUTPUT --filetype pdb 
```

#### Creating an LMDB dataset using silent files.

From command line:
```
python atom3d/torch/dataset.py PATH_TO_PDB_DIR PATH_TO_LMDB_OUTPUT --filetype pdb 
```

#### Loading an LMDB dataset.

From python:
```
from atom3d.torch import LMDBDataset

dataset = LMDBDataset(PATH_TO_LMDB)
# Print length
print(len(dataset))
# Print i-th entry
i = 2
print(dataset[i])
```

### Sharded datasets.

An HDF5 based data format that allows for keyed indexing of structures.

### Loading a sharded dataset.

From python:
```
import atom3d.shard.shard as sh

# Load dataset split into fragments (or shards).
sharded = sh.Sharded.load('sharded/candidates/structures@21')

# Iterate through shards.
for shard_num in range(sharded.get_num_shards()):
  structures = sharded.read_shard(shard_num)
  # You can also load associated metadata.
  labels = sharded.read_shard(shard_num, 'labels')
```

## Contribute

* Issue Tracker: https://github.com/drorlab/atom3d/issues
* Source Code: https://github.com/drorlab/atom3d

## Support

If you are having issues, please let us know.
We have a mailing list located at: atom3d@googlegroups.com

## License

The project is licensed under the MIT license.
