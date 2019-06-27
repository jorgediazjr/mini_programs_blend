# Mini Programs Blend

These mini programs help in the analysis of files produced from running "blend -a" and/or "blend -s"

These additionals programs will only work if you have atleast executed blend in analysis mode.

## good_crystal program

### How does good_crystal work?

FILES NEEDED:
1. CLUSTERS.txt
	- file is produced after executing the following: `blend -a original.dat` 

PROGRAM OPTIONS:
```
usage: good_clusters [-h] [-m MINIMUM] [-x MAXIMUM] [-s SHORT] [-t TALL] [-d]

This program accepts short and tall heights of cluster(s),
OR it accepts minimum and maximum number of datasets
per cluster.

Helps user extract promising clusters.

optional arguments:
  -h, --help            show this help message and exit
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
  -d, --dataset         If this is entered then minimum and maximum are used
```
