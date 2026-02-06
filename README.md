# shirp_elasmos

A repo for Shinnecock Bay Restoration Program (ShiRP) elasmobranch eDNA project and manuscript.

Bioinformatics according to [REVAMP](https://github.com/McAllister-NOAA/REVAMP)

Reference database generated with [RCrux](https://github.com/CalCOFI/rCRUX) and available at [OSF](TBD)

FastQ files are available under [Bioproject #](TBD)

To run revamp:

2021:

```
revamp.sh -p 01_config_file_Elas02-2021.txt -f 02_figure_config_file_Elas02-2021.txt -s 03_sample_metadata_Elas02-2021.txt -r raw_data/2021-Elas02 -o results/revamp-2021-Elas02/
```

2023:

```
revamp.sh -p 01_config_file_Elas02-2023.txt -f 02_figure_config_file_Elas02-2023.txt -s 03_sample_metadata_Elas02-2023.txt -r raw_data/2023-Elas02/demux -o results/revamp-2023-Elas02/
```




