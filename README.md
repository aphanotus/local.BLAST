# Local BLAST

This document describes how to run command-line [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279680/) with custom search-able databases on [Colby's **nscc**](https://www.colby.edu/arc/hardwaresystems/computer-clusters/nscc/).

## Running BLAST on **nscc**

"[BLAST+](https://www.ncbi.nlm.nih.gov/books/NBK279690/)" is a suite of linux programs that run the different variations of the [basic local alignment search tool (BLAST) algorithm](https://en.wikipedia.org/wiki/BLAST). Which program (`blastn`, `blastp`, `blastx` or `tblastn`) you need to run depends to whether your search query is a nucleotide or amino acid (protein) sequence and whether you're searching a database of nucleotide or protein sequences.

![BLAST varieties](https://www.bugsinourbackyard.org/wp-content/uploads/2018/06/blast.types_.jpg)

Once you know the variety of BLAST you need, the basic form of the command is:

```
blastn -query /path/input.filename.fa -db /path/BLASTdb > output.filename
```

Notice that the default is for BLAST to send its output to "stdout", that is, the screen. So typically you want to redirect that output to a named file.

Here's a more realistic example.

```
tblastn -query /research/drangeli/BLAST_DBs/query_sequences/Dmel.act5C.fa \
  -db /research/drangeli/BLAST_DBs/Nlug.CDS.BLASTdb/Nlug.OGSv1-0.CDS.BLASTdb \
  > Dmel.act5c.vs.Nlug.OGSv1-0.CDS.tblastn.txt
```

Notice a few things about this command.

* The input files are all identified by their complete path from root. I do this because the query files and the databases are typically in different folders, and this keep things organized. 
* The output file has no path. In other words the i,mplied path is `./`. So, I typically run the BLAST command from the folder where I want the output file to be.
* The output file name has built into it several important pieces of information:
	+ the name of query sequence,  `Dmel.act5C`, in this example
	+ the name of the database,  `Nlug.OGSv1-0.CDS`
	+ the type of BLAST, `tblastn`
	+ the `.txt` extension should make it clear that this is human-readable output

### A note on digital species abbreviations 

In order to keep things organized on **nscc**, it's helpful to use consistent and clear file names. For species, they are typically identified by a four letter abbreviation consisting of the first initial of the genus, followed by the first three letters of the specific epithet. So, *Oncopeltus fasciatus* becomes `Ofas`.

There are a few exceptions to this rule. The pea aphid, *Acyrthosiphon pisum*, would become `Apis`, which would certainly get confused with the honeybee genus, *Apis*. So the aphid community has adopted `Acypi` as their digital handle.

## Custom BLAST databases

Below is a list of paths to each of the custom [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279680/) search-able databases available to our lab group on `nscc`. Custom BLAST databases each reside in a folder, but consist of several different files (with the extensions `nhr`, `nin`, `nog`, `nsd`, `nsi`, and `nsq`). To run [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279680/) from the linux command line, you will need to refer to the path of the database and the base name of those files. List the contents of the database folder if you're not sure what this looks like.



### *Oncopeltus fasciatus*

This is the reference transcriptome that was used to annotate the *O. fasciatus* genome project. The CDS (coding sequence) FASTA file was kindly provided by [Kristen Panfilio](https://warwick.ac.uk/fac/sci/lifesci/people/kpanfilio/). When she shared the file, Kristen told us the data originate from "pooled Illumina RNAseq reads from mixed juvenile, adult male, and adult female libraries". But we have no more specific information about the ages of those individuals. We might be able to follow-up with Kristen about that.

```
/research/drangeli/BLAST_DBs/Ofas_transdecoder_cds/Ofas.TR.BLASTdb
```

### *Jadera haematoloma*

This database is built from the 'grand union' of transcripts assembled from samples of the Plantation Key ecotype from whole bodies, dorsal thorax and gonads of first day adults. It is the most complete *J. haematoloma* transcriptome we have and is estimated (by [BUSCO](https://busco.ezlab.org/)) to include 89% of conserved genes.

```
/research/drangeli/BLAST_DBs/Jhae_GU_BLAST_DB/Jhae.GU.TRassembly.BLASTdb
```

Additionally, we have transcriptomes and BLAST databases for samples from male and female gonads (testes and ovaries). I'm not sure if the testes also included the accessory glands.

#### *J. haematoloma* females

```
/research/drangeli/BLAST_DBs/Jhae_ovary_BLAST_database/Jhae.ovary.TRassembly.BLASTdb
```

#### *J. haematoloma* males

```
/research/drangeli/BLAST_DBs/Jhae_testes_BLAST_database/Jhae.testes.TRassembly.BLASTdb
```
### *Jadera sanguinolenta*

[*J. sanguinolenta*](http://www.soapberrybug.org/01_cms/details.asp?ID=72) is a seperate species of soapberry bug whose range overlaps that of [*J. haematoloma*](http://www.soapberrybug.org/01_cms/details.asp?ID=65) in South Florida. They are not know to hybridize in the wild and attempts to do so in the lab have not produced offspring. *J. sanguinolenta* is not known to produce short-wing morphs in the wild, but they have appeared in the lab, suggesting a hidden reaction norm.

At the time we made this transcriptome, we thought the identification of this bug might have been [*Jadera hinnulea*](http://www.soapberrybug.org/01_cms/details.asp?ID=60), which is why these files are labeled `Jhin` rather than `Jsan`. (I'd rename that, but I'm afraid the contents of these files might refer to their own file names, which would cause problems. Eventually, we should just re-build the BLAST database, so eliminate that name issue.)

```
/research/drangeli/BLAST_DBs/Jhae_GU_BLAST_DB/Jhae.GU.TRassembly.BLASTdb
```

### *Boisea trivittata*

The [eastern box elder bug, *Boisea trivittata*](https://upload.wikimedia.org/wikipedia/commons/4/44/Eastern_Boxelder_Bug_-_Flickr_-_treegrow.jpg), is the only rhopalid native to northeastern North America. Our lab created a transcriptome for this species with individuals collected in [Waterville, ME](https://www.google.com/maps/place/44%C2%B033'34.6%22N+69%C2%B037'51.9%22W/).

```
/research/drangeli/BLAST_DBs/Btri_BLAST_database/Btri.TRassembly.BLASTdb
```

### Other Hemiptera

The [USDA i5k project](https://i5k.nal.usda.gov/) has a number of other genome projects in the works for Hemiptera at various stages of completion. There are currently five species with transcriptomes available, and I've made BLAST databases from these. 

#### A note on taxonomy

To understand how these species might be useful, it's helpful to have some idea of the phylogenetic relationships of these species as well as their unique features. Unfortunately, the taxonomy of true bugs is a mess. Mid-century entomologists recognised two orders: Heteroptera, the true bugs, and [Homoptera](https://en.wikipedia.org/wiki/Homoptera), the cicadas and their allies. However, [molecular phylogenetics](http://science.sciencemag.org/content/346/6210/763/tab-figures-data) has found that Heteroptera is nested within what used to be 'Homoptera'. So the term 'Homoptera' is now defunct, and people recognise a single order Hemiptera, with 3 suborders: [Heteroptera](https://en.wikipedia.org/wiki/Heteroptera) (the same name with the same species in it), [Auchenorrhyncha](https://en.wikipedia.org/wiki/Auchenorrhyncha) (cicadas, leafhoppers, treehoppers, planthoppers, and spittlebugs) and [Sternorrhyncha](https://en.wikipedia.org/wiki/Sternorrhyncha) (aphids, whiteflies, and scale insects).

Here's a [figure](https://ars.els-cdn.com/content/image/1-s2.0-S2214574517301153-gr2.jpg) Kristen and I produced for a review we wrote on [hemipteran genomics](https://www.sciencedirect.com/science/article/pii/S2214574517301153). Below these species are listed in decreasing relatedness to *Oncopeltus*.

![Genomeic resources for Hemiptera and their relationships](https://ars.els-cdn.com/content/image/1-s2.0-S2214574517301153-gr2.jpg)

#### *Halyomorpha halys* 

The invasive [brown marmorated stink bug](https://en.wikipedia.org/wiki/Brown_marmorated_stink_bug) is a member of the [Pentatomomorpha](https://en.wikipedia.org/wiki/Pentatomomorpha), the infraorder that includes *Oncopeltus* (family [Lygaeidae](https://en.wikipedia.org/wiki/Lygaeidae) and *Jadera* (family [Rhopalidae](https://en.wikipedia.org/wiki/Rhopalidae)).

```
/research/drangeli/BLAST_DBs/Hhal.CDS.BLASTdb/Hhal.BCMv0-5-3.CDS.BLASTdb
```

#### *Cimex lectularius*

The [bedbug](https://en.wikipedia.org/wiki/Cimex_lectularius) represents the infraorder [Cimicomorpha](https://en.wikipedia.org/wiki/Cimicomorpha).

```
/research/drangeli/BLAST_DBs/Clec.CDS.BLASTdb/Clec.OGSv1-2.CDS.BLASTdb
```

#### *Gerris buenoi*

The [water strider](https://i5k.nal.usda.gov/Gerris_buenoi) represents the infraorder [Gerromorpha](https://en.wikipedia.org/wiki/Gerromorpha), the earliest diverging lineage of the Heteroptera. 

```
/research/drangeli/BLAST_DBs/Gbue.CDS.BLASTdb/Gbue.OGSv1-0.CDS.BLASTdb
```

#### *Nilaparvata lugens*

The [brown planthopper](https://en.wikipedia.org/wiki/Brown_planthopper) is currently the only member of the [Auchenorrhyncha](https://en.wikipedia.org/wiki/Auchenorrhyncha) with an available transcriptome. 

```
/research/drangeli/BLAST_DBs/Nlug.CDS.BLASTdb/Nlug.OGSv1-0.CDS.BLASTdb
```

#### *Acyrthosiphon pisum*

The [pea pahid genome](https://www.hgsc.bcm.edu/arthropods/aphid-genome-project) was one of the first big insect genome projects. This pest represents the [Sternorrhyncha](https://en.wikipedia.org/wiki/Sternorrhyncha), the earliest-branching major lineage of Hemiptera. 

```
/research/drangeli/BLAST_DBs/Acypi.CDS.BLASTdb/Acypi.OGSv2-1b.CDS.BLASTdb
```

#### *Pachypsylla venusta*

[*Pachypsylla venusta*](https://i5k.nal.usda.gov/Pachypsylla_venusta) is a gall-forming [psyllid](https://en.wikipedia.org/wiki/Jumping_plant_louse). This species represents a relatively early-branching lineage within the [Sternorrhyncha](https://en.wikipedia.org/wiki/Sternorrhyncha).

```
/research/drangeli/BLAST_DBs/Pven.CDS.BLASTdb/Pven.BCMv0-5-3.CDS.BLASTdb
```

#### *Frankliniella occidentalis*

Thrips such as [*F. occidentalis*](https://i5k.nal.usda.gov/Frankliniella_occidentalis) are members of the [Phthiraptera](https://en.wikipedia.org/wiki/Phthiraptera), the sister-order to the [Hemiptera](https://en.wikipedia.org/wiki/Hemiptera).

```
/research/drangeli/BLAST_DBs/Focc.CDS.BLASTdb/Focc.BCMv0-5-3.CDS.BLASTdb
```

## BLAST parameters

The default output for local BLAST is a human-readable tabular format, give a long list of matches, including some that are very poor. However, you can adjust BLAST's output with some additional parameters in the command line. The [BLAST+ manual](https://www.ncbi.nlm.nih.gov/books/NBK279684/) has detailed information on all the suite's functionality. But here's a summary of some useful switches. These switches can be used in combination with one another.

### Filter by E-value

```
blastn -query /path/input.filename.fa -db /path/BLASTdb \
  -evalue 1e-10 \
  > output.filename
```

### Set a limit on the number of target sequences

```
blastn -query /path/input.filename.fa -db /path/BLASTdb \
  -max_target_seqs 10 \
  > output.filename
```

This will limit the output to the top 10 matches.

### Limit the number of alignments BLAST will return for each query-subject pair

It's possible for a query search and a subject sequence to align more of less well along different stretches. This is most relevant when the database includes very long sequences, that might have tandem duplications. This output can be reduced to show only the best such alignments. The example below will report only the best alignment between any query and subject sequence pair. 

```
blastn -query /path/input.filename.fa -db /path/BLASTdb \
  -max_hsps 1 \
  > output.filename
```

### Run BLAST using multiple processors

**nscc** is a multi-processor computing cluster. By default, most programs will use only one processor, but you can direct many of them to "multi-thread" and use multiple processors simultaneously.

Do this only with caution, since it will impact other users on **nscc**. As a rule, you should only use multi-threading on node 26. The biology node has 32 processors, and as a courtesy to other users, it's good form to use at most half of those at any time. The example below uses 16 processors. 

```
blastn -query /path/input.filename.fa -db /path/BLASTdb \
  -num_threads 16 \
  > output.filename
```

### Change the output format

BLAST has the ability to render its output in format other than the default table and alignment. Several options are possible, and they're described in Table C1 in the Appendix to the [BLAST+ manual](https://www.ncbi.nlm.nih.gov/books/NBK279684/).  If you look at this table, scroll down or search for the `outfmt` entry.

For many big data bioinformatics approaches, it can be useful to get your BLAST output in a TSV format that can be imported into R or other applications.  One line per result is produced with  `-outfmt 6`. But you'll want to specify exactly which metadata the BLAST returns. They are specified in double quotes, as in the example below.

```
blastn -query /path/input.filename.fa -db /path/BLASTdb \
  -evalue 1e-10 -max_target_seqs 10 -max_hsps 1 -num_threads 16 \
  -outfmt "6 qseqid sseqid pident qlen length mismatch evalue bitscore" \
  > output.filename
```

----
-*Dave Angelini*, 2018
