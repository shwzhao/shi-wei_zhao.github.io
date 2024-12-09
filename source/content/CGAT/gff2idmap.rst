gff2idmap
=========

.. code-block:: console

   cgat gff2idmap -h

   usage: cgat gff2idmap [-h] -g GFF_FILE [-o OUTPUT_FILE] [-t TRANS_MRNA_INFO_TO] [-e EXTRA_INFO]
                         [--only_coding_gene]

   options:
     -h, --help            show this help message and exit
     -g GFF_FILE, --gff_file GFF_FILE
                           Path to gff file
     -o OUTPUT_FILE, --output_file OUTPUT_FILE
                           Path to the output file. [id_mapping.txt]
     -t TRANS_MRNA_INFO_TO, --trans_mRNA_info_to TRANS_MRNA_INFO_TO
                           Transcript or mRNA. [mRNA]
     -e EXTRA_INFO, --extra_info EXTRA_INFO
                           Extra information that you need, for example: -e "mRNA::Dbxref;gene::gbkey". [NULL]
     --only_coding_gene    only map pep coding gene ID

Basic Usage
-----------

.. code-block:: console

   cgat gff2idmap \
     -g example/GCF_000002775.5_P.trichocarpa_v4.1_genomic.gff.gz

   head -5 id_mapping.txt
   ## #gene_id        gene_name       transcript_id   transcript_name cds_id  SeqID   Start   End     Strand
   ## gene-LOC7483226 LOC7483226      rna-XM_002299051.3      XM_002299051.3  cds-XP_002299087.1      NC_037285.2     40829   43223   -
   ## gene-LOC7457680 LOC7457680      rna-XM_002297573.4      XM_002297573.4  cds-XP_002297609.3      NC_037285.2     50624   52700   +
   ## gene-LOC7483220 LOC7483220      rna-XM_006368463.3      XM_006368463.3  cds-XP_006368525.3      NC_037285.2     60500   65314   -
   ## gene-LOC7457681 LOC7457681      rna-XM_024603583.2      XM_024603583.2  cds-XP_024459351.2      NC_037285.2     65961   72394   -

Additional Options
------------------

You can also output extra information you want:

.. code-block:: console

   cgat gff2idmap \
     -g example/GCF_000002775.5_P.trichocarpa_v4.1_genomic.gff.gz \
     -e "gene::Dbxref;mRNA::experiment"

   head -5 id_mapping.txt
   ## #gene_id        gene_name       transcript_id   transcript_name cds_id  SeqID   Start   End     Strand  gene::Dbxref    mRNA::experiment
   ## gene-LOC7483226 LOC7483226      rna-XM_002299051.3      XM_002299051.3  cds-XP_002299087.1      NC_037285.2     40829   43223   -       GeneID:7483226  COORDINATES: polyA evidence [ECO:0006239]
   ## gene-LOC7457680 LOC7457680      rna-XM_002297573.4      XM_002297573.4  cds-XP_002297609.3      NC_037285.2     50624   52700   +       GeneID:7457680  COORDINATES: polyA evidence [ECO:0006239]
  