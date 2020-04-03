## Metagenome Assembly Pipeline Using ONT Long Reads

### Sample information

1. The DNA was extracted from 11 bacterial aggregates called pink berries using the [CTAB extraction method](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/protocols/DNAextraction/CTAB-DNA-extraction-Protocol.pdf). 

2. The initial DNA sample called **GS11_pool**, diluted at a ratio of 1:10, was quality checked using the three routine methods below. The diluted DNA was used only for quality checks and the library was prepared using the undiluted DNA sample.

	a. <span style="color: blue;">Qubit Fluorometer 4.0</span>: the sample contained DNA at a concentration of 39.8 ng/&#956;l.
	
	b. <span style="color: blue;">NanoDrop Spectrophotometer</span>: the 260/230 and 260/280 purity ratios were 2.14 and 2.04, respectively, for this sample.
	
	c. <span style="color: blue;">Aligent TapeStation 2200</span>: the sample had a DIN value of 8.0 and a DNA concentration of 22.9 ng/&#956;l. The full TapeStation results are located [here](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/TapeStation-Results/0_CTAB_extraction_tests_TapeStationResults_09Sep2019.pdf). 
	
3. We ran an initial library using the undiluted **GS11_pool** sample and SQK-LSK108 kit. The pore occupancy decreased very rapdily within the first few hours of the run. Considering the poor quality of results, we RNase treated and sheared our DNA for the subsquent sequencing run (see shearing info below). The [run report](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/minion-run-reports/report_FAL40909_20200107_0030_4bbeb7ac_06Jan2020.pdf) and the [TapeStation results for the library](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/TapeStation-Results/1_GS11_pool-library-TapeStationResults-14Jan2020.pdf) are available on this repo. 

4. This pipeline utilizes that sequencing data for the above **GS11_pool** sample that was RNase treated as described at the end of the [CTAB extraction method](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/protocols/DNAextraction/CTAB-DNA-extraction-Protocol.pdf). After this treatment, the purified DNA was quality checked again using the three routine methods below.

	a. <span style="color: blue;">Qubit Fluorometer 4.0</span>: the sample contained DNA at a concentration of <span style="color: red;">**NUM**</span> ng/&#956;l.
	
	b. <span style="color: blue;">NanoDrop Spectrophotometer</span>: the 260/230 and 260/280 purity ratios were <span style="color: red;">**NUM**</span> and <span style="color: red;">**NUM**</span>, respectively, for this sample. <span style="color: red;">**We may not have these NUMs**</span>
	
	c. <span style="color: blue;">Aligent TapeStation 2200</span>: the sample had a DIN value of 7.8 and a DNA concentration of 13.7 ng/&#956;l (Sample Description: GS11 Pool RNase treated before shearing). We sheared the DNA for 1 min at 6000 rpm (twice total) using the Eppendorf 5424 centrifuge (Sample Description: GS11 Pool RNase treated after shearing). The full TapeStation results are located [here](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/TapeStation-Results/2_GS11_pool_RNaseTreated_Sheared1x_03Feb2020.pdf).

5. The shearing of our sample at 6000 rpm for 1 min (twice total) resulted in average fragment length of 23,419 bp (see TapeStation results from 03 Feb 2020). Therefore, we sheared this DNA again for the same time but at a higher speed of 8000 rpm. The second shearing step resulted in an average fragment of 12,975 bp. See [TapeStation results from 11 Feb 2020](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/TapeStation-Results/3_2_GS11_pool_RNaseTreated_Sheared2x_11Feb2020.pdf) (Sample Description: GS11\_pool\_2nd\_shearing\_8k). 

6. <span style="color: purple;">**So, the DNA concentration of the sample used for sequencing was 25.6 ng/&#956;l (DIN value: 7.4) with an average fragment length of 12,975 bp.**</span>
     
---
---
### Library information
We followed the library preparation protocol per the manufacturer instructions for sequencing **Genomic DNA by Ligation (SQK-LSK109)**. Before are DNA concentrations after each major step in the protocol. The TapeStation results for the final library are [here](https://github.com/tarunaaggarwal/ont-metagenome-assembly-pipeline/blob/master/TapeStation-Results/4_GS11_pool_RNaseTreated_Sheared_DNA_Library_12Feb2020.pdf).

1. Total starting DNA concentration (measured on the TapeStation): 1.152 &#956;g (1,152 ng)
2. Total DNA concentration after **DNA repair and end-prep** (measured on Qubit)): 954 ng (15.9 ng/&#956;l) 
3. Total DNA concentration after **Adapter ligation and clean-up** (measured on the TapeStation): 512.4 ng (36.6 ng/&#956;l)  
4. In order to meet ONT's recommendations of loading 5-50 fmol of the final prepared library, we used <span style="color: red;">**NUM**</span> &#956;l of our library which amounts to <span style="color: red;">**NUM**</span> fmol.


---
---
### Flow cell and kit information
* Instrument ID: MN28992
* Flowcell: FLO-MIN106 
* Flowcell ID: FAL76976
* Kit: SQK-LSK109

---
---
### Sequencing run information
* Sample ID: GS11\_pooled\_sheared_DNA
* Protocol Group ID: GS11\_pooled\_sheared\_DNA
* Sequencing started: 12 Feb 2020 at 15:48 local time (Pacific Standard)
* Processing stopped: 14 Feb 2020 at 11:11 local time (Pacific Standard)
* Total run time: 43 hours and 23 minutes 

---
---

### Raw data and run files location
The `fact5` and files generated during the run are located on the lab iMac in `/Library/MinKNOW/data/GS11_pooled_sheared_DNA/GS11_pooled_sheared_DNA/20200212_2347_MN28992_FAL76976_637c6cee/`

---
---

### Assembly Pipeline
#### Step 1: Basecall the raw fast5 files with Guppy
Version used in this pipeline: 

```
guppy_basecaller \
--flowcell FLO-MIN106 \
--kit SQK-LSK109 \
--input_path /home/hdore/berries/nanopore_sequencing/GS11_pool_sheared_12Feb2020_2/raw_data/20200212_2347_MN28992_FAL76976_637c6cee/fast5 \
--save_path . \
--num_callers 8 \
--ipc_threads 16
```

#### Step 2: Remove barcodes. Remember that barcodes and adapters are two different things. If there are no barcoded samples, then using guppy_barcoder or qcat will do no good. Adapters and barcodes are trimmed by those tools if barcodes are found. ONT suggests we use soft-clipping options within the assembly tool we choose to use. 

---
---

