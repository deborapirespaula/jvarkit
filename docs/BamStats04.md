# BamStats04

Coverage statistics for a BED file.


## Usage

```
Usage: bamstats04 [options] Files
  Options:
  * -B, --bed
      Bed File. Required
    -cov, --cov
      min coverage to say the position is not covered
      Default: 0
    -f, --filter
      A filter expression. Reads matching the expression will be filtered-out. 
      Empty String means 'filter out nothing/Accept all'. See https://github.com/lindenb/jvarkit/blob/master/src/main/resources/javacc/com/github/lindenb/jvarkit/util/bio/samfilter/SamFilterParser.jj 
      for a complete syntax.
      Default: mapqlt(1) || MapQUnavailable() || Duplicate() || FailsVendorQuality() || NotPrimaryAlignment() || SupplementaryAlignment()
    -h, --help
      print help and exit
    --helpFormat
      What kind of help
      Possible Values: [usage, markdown, xml]
    -o, --output
      Output file. Optional . Default: stdout
    -partition, --partition
      [20171120]Data partitioning using the SAM Read Group (see 
      https://gatkforums.broadinstitute.org/gatk/discussion/6472/ ) . It can 
      be any combination of sample, library....
      Default: sample
      Possible Values: [readgroup, sample, library, platform, center, sample_by_platform, sample_by_center, sample_by_platform_by_center, any]
    -R, --ref
      Indexed fasta Reference file. This file must be indexed with samtools 
      faidx and with picard CreateSequenceDictionary If set, a column with the 
      GC% will be added
    --version
      print version and exit

```


## Keywords

 * sam
 * bam
 * coverage
 * depth
 * statistics
 * bed


## Compilation

### Requirements / Dependencies

* java [compiler SDK 1.8](http://www.oracle.com/technetwork/java/index.html) (**NOT the old java 1.7 or 1.6**) and avoid OpenJdk, use the java from Oracle. Please check that this java is in the `${PATH}`. Setting JAVA_HOME is not enough : (e.g: https://github.com/lindenb/jvarkit/issues/23 )
* GNU Make >= 3.81
* curl/wget
* git
* xsltproc http://xmlsoft.org/XSLT/xsltproc2.html (tested with "libxml 20706, libxslt 10126 and libexslt 815")


### Download and Compile

```bash
$ git clone "https://github.com/lindenb/jvarkit.git"
$ cd jvarkit
$ make bamstats04
```

The *.jar libraries are not included in the main jar file, [so you shouldn't move them](https://github.com/lindenb/jvarkit/issues/15#issuecomment-140099011 ).
The required libraries will be downloaded and installed in the `dist` directory.

Experimental: you can also create a [fat jar](https://stackoverflow.com/questions/19150811/) which contains classes from all the libraries, on which your project depends (it's bigger). Those fat-jar are generated by adding `standalone=yes` to the gnu make command, for example ` make bamstats04 standalone=yes`.

### edit 'local.mk' (optional)

The a file **local.mk** can be created edited to override/add some definitions.

For example it can be used to set the HTTP proxy:

```
http.proxy.host=your.host.com
http.proxy.port=124567
```
## Source code 

[https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/bamstats04/BamStats04.java](https://github.com/lindenb/jvarkit/tree/master/src/main/java/com/github/lindenb/jvarkit/tools/bamstats04/BamStats04.java)


<details>
<summary>Git History</summary>

```
Mon Nov 20 15:01:11 2017 +0100 ; adding partition for bamstats04, Partiton.OPT_DESC ; https://github.com/lindenb/jvarkit/commit/9f4e9dd12ffa66dc87e773bc7afa7040d507bfee
Sun Nov 19 16:21:21 2017 +0100 ; bamstats04 : using percentil and median use MIN_DEPTH ; https://github.com/lindenb/jvarkit/commit/d407ea6d4a08938ef18fa445e5d1205f8d2de723
Thu Nov 16 10:28:49 2017 +0100 ; simplifying bam2wig, minor changes in bam2xml ; https://github.com/lindenb/jvarkit/commit/c1708995bbd50a2e666eebd772d6dff02a4f2d62
Sun May 21 20:02:10 2017 +0200 ; instanceMain -> instanceMainWithExit ; https://github.com/lindenb/jvarkit/commit/4fa41d198fe7e063c92bdedc333cbcdd2b8240aa
Mon May 15 17:17:02 2017 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/fc77d9c9088e4bc4c0033948eafb0d8e592f13fe
Mon May 15 12:10:21 2017 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/b4895dd40d1c34f345cd2807f7a81395ba27e8ee
Fri Apr 21 18:16:07 2017 +0200 ; scan sv ; https://github.com/lindenb/jvarkit/commit/49b99018811ea6a624e3df556627ebdbf3f16eab
Thu Apr 20 17:51:46 2017 +0200 ; continue transition jcommander ; https://github.com/lindenb/jvarkit/commit/c3b0181c8698f30edaed6b0d9e4350cc425f0dd3
Fri Apr 7 16:35:31 2017 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/54c5a476e62e021ad18e7fd0d84bf9e5396c8c96
Mon Jul 25 17:11:31 2016 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/ebfd55df76327f73a3850150ccff303d96256f93
Fri Jul 22 11:47:04 2016 +0200 ; bamstat04 and genomicseq with gc% ; https://github.com/lindenb/jvarkit/commit/ae9355bb3bfb10cfaa88d7a9d0e2650e69e48368
Mon May 30 09:56:31 2016 +0200 ; cont ; https://github.com/lindenb/jvarkit/commit/e7b2fe070bf124c8b71611d621a2efb4d0fab90a
Tue Apr 26 17:21:33 2016 +0200 ; vcfbuffer ; https://github.com/lindenb/jvarkit/commit/3300512769fd3bb2ee4430c9474367b06f2edc7c
Sat Feb 14 15:22:43 2015 +0100 ; cont ; https://github.com/lindenb/jvarkit/commit/d9384ecea57ee772dffddac92dcc24d995005fb3
Tue Jun 10 11:19:47 2014 +0200 ; paired check in bamstats04 ; https://github.com/lindenb/jvarkit/commit/ae922afacbc9355494f361fde1f456d722758100
Tue Jun 10 10:55:46 2014 +0200 ; paired check in bamstats04 ; https://github.com/lindenb/jvarkit/commit/72c4f302902e44df15f20a1d181cb551ef9dba37
Mon May 12 14:06:30 2014 +0200 ; continue moving to htsjdk ; https://github.com/lindenb/jvarkit/commit/011f098b6402da9e204026ee33f3f89d5e0e0355
Mon May 12 10:28:28 2014 +0200 ; first sed on files ; https://github.com/lindenb/jvarkit/commit/79ae202e237f53b7edb94f4326fee79b2f71b8e8
Tue Nov 26 12:29:03 2013 +0100 ; unclipped start -> align start ; https://github.com/lindenb/jvarkit/commit/3944b21281c2b4afc1ef682f0abe020b26940e37
Fri Oct 11 15:39:02 2013 +0200 ; picard v.100: deletion of VcfIterator :-( ; https://github.com/lindenb/jvarkit/commit/e88fab449b04aed40c2ff7f9d0cf8c8b6ab14a31
Fri Sep 27 18:13:12 2013 +0200 ; cont fastq ; https://github.com/lindenb/jvarkit/commit/94e90aea48e4b5c1a08fb81b4871fe3f5d349590
Fri Sep 13 15:09:13 2013 +0200 ; vcf annote with bam ; https://github.com/lindenb/jvarkit/commit/f17a42f7b5e15dfdb0255e422f3dcb72e3aea400
Thu Aug 8 16:06:25 2013 +0200 ; bamstats04 pour solena ; https://github.com/lindenb/jvarkit/commit/791ac07999107af305fa65c3a1d55e6ebc5636b1
Thu Aug 8 16:00:55 2013 +0200 ; bamstats04 pour solena ; https://github.com/lindenb/jvarkit/commit/71cb2217d949df7b72f539d1551fb23d80ce4c0b
Mon May 6 18:56:46 2013 +0200 ; moving to git ; https://github.com/lindenb/jvarkit/commit/55158d13f0950f16c4a3cc3edb92a87905346ee1
```

</details>

## Contribute

- Issue Tracker: [http://github.com/lindenb/jvarkit/issues](http://github.com/lindenb/jvarkit/issues)
- Source Code: [http://github.com/lindenb/jvarkit](http://github.com/lindenb/jvarkit)

## License

The project is licensed under the MIT license.

## Citing

Should you cite **bamstats04** ? [https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md](https://github.com/mr-c/shouldacite/blob/master/should-I-cite-this-software.md)

The current reference is:

[http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)

> Lindenbaum, Pierre (2015): JVarkit: java-based utilities for Bioinformatics. figshare.
> [http://dx.doi.org/10.6084/m9.figshare.1425030](http://dx.doi.org/10.6084/m9.figshare.1425030)


## History

* 2017-11-20: added new column 'partition'
* 2017-11-20: can read more than one BAM File.

## Example

```
$ java -jar dist/bamstats04.jar -B src/test/resources/toy.bed.gz src/test/resources/toy.bam 2> /dev/null | column -t 

#chrom  start  end  length  sample  mincov  maxcov  meancov  mediancov  nocoveragebp  percentcovered
ref     10     13   3       S1      3       3       3.0      3.0        0             100
ref2    1      2    1       S1      2       2       2.0      2.0        0             100
ref2    13     14   1       S1      6       6       6.0      6.0        0             100
ref2    16     17   1       S1      6       6       6.0      6.0        0             100
```

