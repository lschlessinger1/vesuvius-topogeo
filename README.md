# vesuvius-topogeo
Here, you'll find [a notebook](notebooks/00-analyze-all-meshes.ipynb) analyzing the topology and geometry of the fragments and scroll segments for the 
[Vesuvius Challenge](https://scrollprize.org/). The mesh analysis notebook can be found under the `notebooks` directory.

## Getting started

If you'd like to run the notebook, you'll first have to download the dependencies and ensure the mesh data is in the 
expected place.

### Installation

You can install requirements by running:

```bash
pip install -r requirements.txt
````

### Data directory structure

The following structure is required in order to load the mesh data:
```
path/to/scroll/data
│
└───1
│   │
│   └───<segment id>
│       └───<segment id>.obj
│
└───2
    │
    └───<segment id>
        └───<segment id>.obj

path/to/fragment/data
│
├───1
│   └───result.obj
├───2
│   └───result.obj
└───3
    └───result.obj
```

The `path/to/scroll/data` and `path/to/fragment/data` default to `data/fragments` and `data/scrolls` respectively. The 
`data` directory can be changed with the environment variable `DATA_DIR`.

### Downloading data

If you don't have the mesh data, you can download it after you have registered for the 
[Vesuvius Challenge](https://scrollprize.org/) (see [data agreement here](https://docs.google.com/forms/d/e/1FAIpQLSf2lCOCwnO1xo0bc1QdlL0a034Uoe7zyjYBY2k33ZHslHE38Q/viewform)).
This will give you the username and password that you'll need for the next step. You must set the environment variables
`USER` and `PASS`. You can create an `.env` file (see `.env.example` for an example), fill it out. You'd then have to
set the environment variables, which can be done as such in a Linux shell:

```bash
export $(grep -v '^#' .env | tr -d '\r' | xargs)
```

Under the `scripts` directory, there are two scripts: one for downloading the scroll mesh data and one for downloading 
the fragment mesh data. They rely on [rclone](https://rclone.org), so please download it from 
[here](https://rclone.org/downloads/).

To download all fragment mesh data (only `.obj` files) you can run the script:

```bash
./scripts/download-fragment-mesh-data.sh 1 2 3
```

All fragment mesh data will currently require ~20 MB of disk space.

To download all scroll mesh data (only `.obj` files) you can run the script:

```bash
./scripts/download-scroll-mesh-data.sh 1 2
```

All scroll mesh data will currently require ~500 MB of disk space.

The default download directory will be `data`, but this can be changed by setting the `DATA_DIR` environment variable.

## References

> Parsons, S., Parker, C. S., Chapman, C., Hayashida, M., & Seales, W. B. (2023). EduceLab-Scrolls: Verifiable Recovery of Text from Herculaneum Papyri using X-ray CT. arXiv preprint arXiv:2304.02084.