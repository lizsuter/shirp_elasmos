# shirp_elasmos

A repo for Shinnecock Bay Restoration Program (ShiRP) elasmobranch eDNA project and manuscript.

FastQ files are available under [Bioproject #](TBD)

Reference database generated with [RCrux](https://github.com/CalCOFI/rCRUX) and available at [Zenodo](https://zenodo.org/records/18626068)

Useage:

```{r}

dir.create("elas02")

forward_primer_seq = "GTTGGTHAATCTCGTGCCAGC"
reverse_primer_seq =  "CATAGTAGGGTATCTAATCCTAGTTTG"
metabarcode_name <- "elas02" 
blast_db_path <- "NCBI_blast_nt/nt"


get_seeds_local(forward_primer_seq,
                 reverse_primer_seq,
                 metabarcode_name,
                 output_directory_path,
                 accession_taxa_sql_path,
                 blast_db_path, mismatch = 3, max_to_blast = 3)

blast_seeds(seeds_output_path,
            blast_db_path,
            accession_taxa_sql_path,
            output_directory_path,
            metabarcode_name)    



derep_and_clean_db(output_directory_path, summary_path, metabarcode_name)

```

Make into blast-formatted db:


```{bash}

grep -e ">" elas02_derep_and_clean_2.fasta | awk 'sub(/^>/, "")' > AccNos.txt

```

Then generate db using [taxonomizr](https://github.com/sherrillmix/taxonomizr)


```{r}
accNos <-  read.table(file = "elas02/derep_and_clean_db/AccNos.txt", header=FALSE,stringsAsFactors=FALSE)
accessions<-sapply(strsplit(accNos[,1],'\\|'),'[',1)
taxaId<-accessionToTaxa(accessions,"taxonomizr-acc-taxa-Jun2024/accessionTaxa.sql")
mapping_file <- data.frame(accessions, taxaId)
write.table(mapping_file, "elas02/mapping_file.txt", sep='\t', col.names = FALSE, row.names = FALSE, quote=FALSE)

```

Bioinformatics pipeline: [REVAMP](https://github.com/McAllister-NOAA/REVAMP)

Specification are in config files. To run:

2021:

```
revamp.sh -p 01_config_file_Elas02-2021.txt -f 02_figure_config_file_Elas02-2021.txt -s 03_sample_metadata_Elas02-2021.txt -r raw_data/2021-Elas02 -o results/revamp-2021-Elas02/
```

2023:

```
revamp.sh -p 01_config_file_Elas02-2023.txt -f 02_figure_config_file_Elas02-2023.txt -s 03_sample_metadata_Elas02-2023.txt -r raw_data/2023-Elas02/demux -o results/revamp-2023-Elas02/
```




