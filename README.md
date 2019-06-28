# Mini Programs Blend

These mini programs help in the analysis of files produced from running `blend -a original.dat`
and/or `blend -s tallest_height [smallest_height]`

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
