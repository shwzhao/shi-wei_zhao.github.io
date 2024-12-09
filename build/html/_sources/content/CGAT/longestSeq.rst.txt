longestSeq
==========

Use the `id_mapping.txt` file to generate a gene sequence file containing only the longest isoform for each gene. Additionally, you can customize the gene names as needed.

.. code-block:: console

   cgat longestSeq -h

   usage: cgat longestSeq [-h] -i IDMAPPING_FILE -s TRANSCRIPT_FILE [-o OUTPUT_FILE] [-l LENGTH_FILE]
                          [-n NUMBER] [-d]

   options:
     -h, --help            show this help message and exit
     -i IDMAPPING_FILE, --idmapping_file IDMAPPING_FILE
                           Path to the gene-transcript mapping file
     -s TRANSCRIPT_FILE, --transcript_file TRANSCRIPT_FILE
                           Path to the transcript sequences file
     -o OUTPUT_FILE, --output_file OUTPUT_FILE
                           Path to the output file. [output.fa]
     -l LENGTH_FILE, --length_file LENGTH_FILE
                           Path to the output transcript length file. [False]
     -n NUMBER, --number NUMBER
                           Which column you want to map. [2]
     -d, --not_change_name
                           Do not change transcript name to gene name. [False]

If there are no matched names in `id_mapping.txt`, you can change the `id_mapping.txt` column or the FASTA sequence name to fit.

Example
-------

.. code-block:: console

   zcat example/GCF_000002775.5_P.trichocarpa_v4.1_protein.faa.gz | grep ">" | head -3
   ## >NP_001391697.1 caffeoyl-CoA O-methyltransferase 1 [Populus trichocarpa]
   ## >NP_001391698.1 caffeoyl-CoA O-methyltransferase 2 [Populus trichocarpa]
   ## >XP_002297609.3 L-ascorbate oxidase homolog [Populus trichocarpa]

   awk 'BEGIN{OFS="\t"}{gsub(/cds-/, "", $5);print}' id_mapping.txt \
     | cgat longestSeq \
     -i - \
     -s example/GCF_000002775.5_P.trichocarpa_v4.1_protein.faa.gz \
     -o pep.faa \
     -n 5

   grep ">" pep.faa | head -3
   ## >gene-LOC7483226
   ## >gene-LOC7457680
   ## >gene-LOC7483220