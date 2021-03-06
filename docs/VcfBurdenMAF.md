# VcfBurdenMAF

![Last commit](https://img.shields.io/github/last-commit/lindenb/jvarkit.png)

Burden : MAF for Cases / Controls 


## Usage

```
Usage: vcfburdenmaf [options] Files
  Options:
    -gtf, --gtf, --gtFiltered
      [20180117] Ignore FILTERed **Genotype**
      Default: false
    -h, --help
      print help and exit
    --helpFormat
      What kind of help. One of [usage,markdown,xml].
    -c, --homref
      Treat No Call './.' genotypes as HomRef
      Default: false
    -ignoreFiltered, --ignoreFiltered
      [20171031] Don't try to calculate things why variants already FILTERed 
      (faster) 
      Default: false
    -lumpy-su-min, --lumpy-su-min
      [20180117] if variant identified as LUMPy-SV variant. This is the 
      minimal number of 'SU' to consider the genotype as a variant.
      Default: 1
    -maxMAF, --maxMAF, -maxAF, --maxAF
      if MAF of cases OR MAF of control is greater than maxMAF, the the FILTER 
      Column is Filled
      Default: 0.05
    -o, --output
      Output file. Optional . Default: stdout
    -p, --pedigree
      [20180117] Pedigree file. Default: use the pedigree data in the VCF 
      header.A pedigree is a text file delimited with tabs. No header. Columns 
      are (1) Family (2) Individual-ID (3) Father Id or '0' (4) Mother Id or 
      '0' (5) Sex : 1 male/2 female / 0 unknown (6) Status : 0 unaffected, 1 
      affected,-9 unknown
    -pfx, --prefix
      Prefix for FILTER/INFO
      Default: Burden
    --version
      print version and exit

```


## Keywords

 * vcf
 * burden
 * maf
 * case
 * control


## Compilation

### Requirements / Dependencies

* java [compiler SDK 11](https://jdk.java.net/11/). Please check that this java is in the `${PATH}`. Setting JAVA_HOME is not enough : (e.g: https://github.com/lindenb/jvarkit/issues/23 )


### Download and Compile

```bash
$ git clone "https://github.com/lindenb/jvarkit.git"
$ cd jvarkit
$ ./gradlew vcfburdenmaf
```

The java jar file will be installed in the `dist` directory.

## Source code 

[https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/burden/VcfBurdenMAF.java](https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/burden/VcfBurdenMAF.java)


## Contribute

- Issue Tracker: [http://github.com/lindenb/jvarkit/issues](http://github.com/lindenb/jvarkit/issues)
- Source Code: [http://github.com/lindenb/jvarkit](http://github.com/lindenb/jvarkit)

## License

The project is licensed under the MIT license.

## Citing

Should you cite **vcfburdenmaf** ? [https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md](https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md)

The current reference is:

[http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

> Lindenbaum, Pierre (2015): JVarkit: java-based utilities for Bioinformatics. figshare.
> [http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)


Variant in that VCF should have one and **only one** ALT allele. Use [https://github.com/lindenb/jvarkit/wiki/VcfMultiToOneAllele](https://github.com/lindenb/jvarkit/wiki/VcfMultiToOneAllele) if needed.

### Output


#### INFO column

  * **BurdenMAFCas** : MAF cases
  * **BurdenMAFControls** : MAF controls

#### FILTER column

  * **BurdenMAFCas** : MAF for cases  doesn't meet  user's requirements
  * **BurdenMAFControls** : MAF for controls  doesn't meet  user's requirements
  * **BurdenMAFCaseOrControls** : MAF for controls or cases  doesn't meet  user's requirements

# Example

```
bcftools annotate -x 'INFO' src/test/resources/rotavirus_rf.ann.vcf.gz |\
	java -jar dist/vcfburdenmaf.jar --pedigree pedigree.ped

##fileformat=VCFv4.2
##ALT=<ID=*,Description="Represents allele(s) other than observed.">
##FILTER=<ID=BurdenMAFCas,Description="MAF of cases is greater than 0.05">
##FILTER=<ID=BurdenMAFCaseOrControls,Description="MAF of (cases OR controls) is greater than 0.05">
##FILTER=<ID=BurdenMAFControls,Description="MAF of controls is greater than 0.05">
##FILTER=<ID=PASS,Description="All filters passed">
##FORMAT=<ID=GT,Number=1,Type=String,Description="Genotype">
##FORMAT=<ID=PL,Number=G,Type=Integer,Description="List of Phred-scaled genotype likelihoods">
##INFO=<ID=BurdenMAFCas,Number=A,Type=Float,Description="Burden Filter F2. MAF Cases">
##INFO=<ID=BurdenMAFControls,Number=A,Type=Float,Description="Burden Filter F2. MAF Controls">
##contig=<ID=RF01,length=3302>
##contig=<ID=RF02,length=2687>
##contig=<ID=RF03,length=2592>
##contig=<ID=RF04,length=2362>
##contig=<ID=RF05,length=1579>
##contig=<ID=RF06,length=1356>
##contig=<ID=RF07,length=1074>
##contig=<ID=RF08,length=1059>
##contig=<ID=RF09,length=1062>
##contig=<ID=RF10,length=751>
##contig=<ID=RF11,length=666>
#CHROM	POS	ID	REF	ALT	QUAL	FILTER	INFO	FORMAT	S1	S2	S3	S4	S5
RF01	970	.	A	C	48.67	.	BurdenMAFCas=0.00;BurdenMAFControls=0.00	GT:PL	0/0:0,9,47	0/0:0,18,73	0/0:0,18,73	0/0:0,33,116	1/1:95,24,0
RF02	251	.	A	T	21.29	BurdenMAFCaseOrControls;BurdenMAFControls	BurdenMAFCas=0.00;BurdenMAFControls=0.500	GT:PL	0/0:0,15,57	0/1:31,0,5	0/1:31,0,5	0/0:0,9,42	0/0:0,24,69
RF02	578	.	G	A	53	.	BurdenMAFCas=0.00;BurdenMAFControls=0.00	GT:PL	0/0:0,33,122	0/0:0,39,135	0/0:0,39,135	1/1:100,30,0	0/0:0,27,109
RF02	877	.	T	A	3.45	BurdenMAFCas;BurdenMAFCaseOrControls	BurdenMAFCas=0.500;BurdenMAFControls=0.00	GT:PL	0/1:37,0,50	0/0:0,22,116	0/0:0,22,116	0/0:0,21,94	0/0:0,12,62
RF02	1726	.	T	G	8.23	BurdenMAFCaseOrControls;BurdenMAFControls	BurdenMAFCas=0.00;BurdenMAFControls=0.500	GT:PL	0/0:0,18,83	0/1:24,0,40	0/1:24,0,40	0/0:0,27,111	0/0:0,10,78
RF02	1962	.	TACA	TA	33.43	BurdenMAFCas;BurdenMAFCaseOrControls	BurdenMAFCas=0.500;BurdenMAFControls=0.00	GT:PL	0/1:70,0,159	0/0:0,15,225	0/0:0,15,225	0/0:0,27,231	0/0:0,27,168
```

