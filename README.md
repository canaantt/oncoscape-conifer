# oncoscape-conifer

## Quick-start

1. Run CoNIFER analysis step 

From the shell, cd to the directory where you extracted CoNIFER.
```
$ cd conifer
```
Then run:

``` 
python conifer.py  analyze \ 
--probes ../sampledata/probes.txt \ 
--rpkm_dir ../sampledata/RPKM_data/ \
--output analysis.hdf5 \
--svd 6 \
--write_svals singular_values.txt
```

This step carries out the CoNIFER algorithm on the RPKM files in the --rpkm_dir option. Two new files are created: the analysis.hdf5, which is a HDF5 file containig all the SVD-ZRPKM values for all samples in the experiment, as well as the singular_values.txt file containing the singular values from the SVD transformation (These can be plotted as a "scree plot") 

2. Make and Plot calls 

```
$ python conifer.py call \
	--input analysis.hdf5 \
	--output calls.txt
```

This step uses a basic thresholding algorithm to find rare CNVs, and the genomic coordinates are listed in calls.txt. 
Next, to visualize these calls and the underlying data, we will use the plotcalls command to create snapshot views of each region. Make a new directory for the images: 
```
$ mkdir call_images
```

Then run conifer.py plotcalls: 

```
$ python conifer.py plotcalls \
	--input analysis.hdf5 \
	--calls calls.txt \
	--outputdir ./call_images/
```

    