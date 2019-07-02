# Mini Programs Blend

These mini programs help in the analysis of files produced from running `blend -a original.dat`

and/or `blend -s tallest_height [smallest_height]`.

These additionals programs will only work if you have atleast executed blend in analysis mode.

## good_clusters program

Sometimes, a long list of data makes it hard for the user to quickly analyze results.
This program's purpose is meant to facilitate the extraction and analysis of certain
range of clusters or heights of clusters.

### How does good_clusters work?

FILES NEEDED:
1. CLUSTERS.txt
    - file is produced after executing the following: `blend -a original.dat` 

PROGRAM OPTIONS:
```
usage: good_clusters [-h] [-d] [-m MINIMUM] [-x MAXIMUM] [-s SHORT] [-t TALL]

This program accepts short and tall heights of cluster(s),
OR it accepts minimum and maximum number of datasets
per cluster.

Helps user extract promising clusters.

optional arguments:
  -h, --help            show this help message and exit
  -d, --dataset         If this is entered then minimum and maximum are used
  -m MINIMUM, --minimum MINIMUM
                        enter the minimum number of datasets you want per
                        cluster, e.g: good_clusters -m 3 will result in all
                        clusters with a minimum of 3 datasets
  -x MAXIMUM, --maximum MAXIMUM
                        enter the maximum number of datasets you want per
                        cluster, e.g: good_clusters -x 7 will result in all
                        clusters with a maximum of 7 datasets
  -s SHORT, --short SHORT
                        enter short height to use with blend synthesis
  -t TALL, --tall TALL  enter tall height to use with blend synthesis
```

FILES PRODUCED:
1. PROMISING_CLUSTERS.txt
    - list of all clusters that are either between a minimum and maximum number of datasets
    OR, list of all clusters that are between a short cluster height or tall cluster height
    - see options above for more information

2. PROMISING_CLUSTERS_HEIGHTS.txt
    - this file has two columns, column 1 contains all the clusters that were extracted and
    found in PROMISING_CLUSTERS.txt. Column 2 contains the heights of each associated cluster

## crystals_blend program

This program helps extract information of the cells that make up each cluster.

Cell information: crystal number, spacegroup number, a, b, c, alpha, beta, gamma, completeness, redundancy

### How does crystals_blend work?

1. FILES NEEDED:
    - BLEND_SUMMARY.txt
        - this is file that contains the crystal numbers with the cell information
        - each crystal represents results from each data set processed
        - clusters are made up of 2 or more crystals 
    - CLUSTERS.txt
        - this is the file that contains the clusters with the crystals that make up each of the clusters

PROGRAM OPTIONS:
```
usage: crystals_blend [-h] [-r] [-c CLUSTERS [CLUSTERS ...]] [-m MINIMUM]
                      [-x MAXIMUM]

This program has a few functionalites based on user taste. If you desire to
run this program, you must have at least the following files:
BLEND_SUMMARY.txt, CLUSTERS.txt, which are produced after running blend -a on
a dataset. MERGING_STATISTICS.info is an optional file, but if it exists, it
will be useful. This program extracts the information on the clusters and
dataset ids from CLUSTERS.txt. Afterwards, this program looks in
BLEND_SUMMARY.txt to extract information on crystal: a, b, c, alpha, beta,
gamma. If MERGING_STATISTICS.info exists, then it will also be able to find
the completeness and redundancy of the cluster. NOTE: If the --read option is
used, you must use the good_clusters program beforehand, in order to produce
the PROMISING_CLUSTERS.txt file, otherwise it will not work.

optional arguments:
  -h, --help            show this help message and exit
  -r, --read            if this option is selected, then program looks for
                        PROMISING_CLUSTERS.txt which is produced from
                        good_clusters program
  -c CLUSTERS [CLUSTERS ...], --clusters CLUSTERS [CLUSTERS ...]
                        enter the cluster(s) you want information on
  -m MINIMUM, --minimum MINIMUM
                        enter lowest number for range of clusters
  -x MAXIMUM, --maximum MAXIMUM
                        enter highest number for range of clusters
```

FILES PRODUCED:
1. CLUSTER_CRYSTAL.info
    - this file contains the cluster(s) with all the crystals
    that make up the cluster(s) and cell information (as mentioned before)

## optimal_data_blend

Program extracts full paths for each data id (crystal) that are in the clusters:
either these clusters are user specified and search for in `CLUSTERS.txt` or
if user has executed `good_clusters` then the file `PROMISING_CLUSTERS.txt` can
be used for this program. 

Another addition that is being worked on is to use information produced from
`random_clusters` which is not finished yet.

### How does optimal_data_blend work?

1. FILES NEEDED:
    - CLUSTERS.txt
        - file produced from running `blend` in analysis mode beforehand
        - contains all necessary information of the clusters program will work with
    - FINAL_list_of_files.dat
        - this information has all the paths that were used for the intial run
        of `blend -a original.dat`
    - PROMISING_CLUSTERS.txt
        - file produced from running `good_clusters`
        - a subset of `CLUSTERS.txt`
        - contains specific clusters
    - RANDOM_CLUSTERS.txt
        - file produced from running `random_clusters` (still being worked on)

PROGRAM OPTIONS:
```
usage: optimal_data_blend [-h] [-c CLUSTERS [CLUSTERS ...]] [-r]

This program finds the path of every crystal in clusters. These clusters can
either be user input OR can be found in PROMISING_CLUSTERS.txt. After finding
the paths the program write each path to a new file inside a new directory.
The user can then run blend analysis mode and analyze the results.

optional arguments:
  -h, --help            show this help message and exit
  -c CLUSTERS [CLUSTERS ...], --clusters CLUSTERS [CLUSTERS ...]
                        enter the cluster(s) you want information on
  -r, --read            this reads RANDOM_CLUSTERS.txt
```

FILES PRODUCED:
1. original.dat
    - file with all paths relating to each data id (crystal) in clusters
    - a directory with the format `new_final_list_hour_minute_second` and
    file saved inside new directory for processing
