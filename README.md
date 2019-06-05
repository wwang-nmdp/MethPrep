# MethylPrep

It's a python application to calculate methylation levels from .cov (coverage) files based on specific ranges.

Quick start
-----------
Find the [latest stable release](https://github.com/wwang-nmdp/MethylPrep/tree/master), download it.
```unix
git clone https://github.com/wwang-nmdp/MethylPrep.git
```
You will need a .txt file to specify the ranges in format of:
```unix
CHR START END Symbol
chr10	10796	47335	gene1
...
chr10	451100 476335	gene4
```
And an input folder to put all the coverage files.
The coverage file was pre-processed by MehtyPrep-filter to elinimate low counts data.

The coverage format includes six columns:
*Chromosomes* *POS* *POS* *Methylation rate* *Methylated cytosines* *UnMethylated cytosines*

For example:
```unix
chr10	10780	10780	66.6666666666667	6	3
chr10	10782	10782	77.7777777777778	7	2
chr10	10790	10790	66.6666666666667	6	3
chr10	10792	10792	44.4444444444444	4	5
chr10	10796	10796	88.8888888888889	8	1
chr10	10802	10802	100	9	0
chr10	10815	10815	77.7777777777778	7	2
```

Once you have range file and input files ready, run the command:
```unix
~$ python ~/methylPrep.py ~/range.txt ~/input ~/output/output.txt

finish read range
process folder input
Finish read /Users/wwang/git/MethylPrep/input/bismark.cov
Find symbols in /Users/wwang/git/MethylPrep/input/bismark.cov
```
The output file covers 1) the counts of signals which identified in range, 2) Methylation level in range. This will help to normalize the data based on the number of methylation signals in the ranges.
Each row represents each individula input coverage files.
Multiple colums represent different ranges.

For example:
To identify the methylation levels of genes which involved in RAS signaling pathway.
```unix
FGF1
FGF2
EGF
AKT1
INS
INSR
HRAS
IGF1R
KDR
```
Build a range file based on provided gene symbols:

```unix
CHR	START	END	INFO
chr4	55991762	55991962	uc003has.3_up_200_chr4_55991763_r
chr4	55991762	55991962	uc003hat.1_up_200_chr4_55991763_r
chr4	110833839	110834039	uc003hzy.4_up_200_chr4_110833840_f
chr4	123747662	123747862	uc003iev.1_up_200_chr4_123747663_f
...
chr19	7294011	7294211	uc002mgf.3_up_200_chr19_7294012_r
```

Run MethylPrep:
```unix
:~$ python ~/methylPrep.py ~/RAS_Key_Genes_200upStream.txt ~input ~/RAS-Key-genes-test-output.txt

finish read range
process folder input
Finish read bismark.cov
Find symbols in bismark.cov

:~$ cat RAS-Key-genes-test-output.txt

fileName	uc003has.3_up_200_chr4_55991763_r_count	uc003has.3_up_200_chr4_55991763_r_ratio	uc003hat.1_up_200_chr4_55991763_r_count	uc003hat.1_up_200_chr4_55991763_r_ratio	uc003hzy.4_up_200_chr4_110833840_f_count	uc003hzy.4_up_200_chr4_110833840_f_ratio	uc003iev.1_up_200_chr4_123747663_f_count	uc003iev.1_up_200_chr4_123747663_f_ratio	uc010imk.3_up_200_chr4_110901633_f_count	uc010imk.3_up_200_chr4_110901633_f_ratio	uc011bzx.2_up_200_chr4_55991763_r_count	uc011bzx.2_up_200_chr4_55991763_r_ratio	uc011cfu.2_up_200_chr4_110833840_f_count	uc011cfu.2_up_200_chr4_110833840_f_ratio	uc011cfv.2_up_200_chr4_110833840_f_count	uc011cfv.2_up_200_chr4_110833840_f_ratio	uc003lmm.4_up_200_chr5_142000921_r_count	uc003lmm.4_up_200_chr5_142000921_r_ratio	uc003lmn.5_up_200_chr5_142066061_r_count	uc003lmn.5_up_200_chr5_142066061_r_ratio	uc003lmp.5_up_200_chr5_142066061_r_count	uc003lmp.5_up_200_chr5_142066061_r_ratio	uc003lmq.3_up_200_chr5_142077636_r_count	uc003lmq.3_up_200_chr5_142077636_r_ratio	uc003lmr.3_up_200_chr5_142077636_r_count	uc003lmr.3_up_200_chr5_142077636_r_ratio	uc003lms.4_up_200_chr5_142077636_r_count	uc003lms.4_up_200_chr5_142077636_r_ratio	uc010jgj.3_up_200_chr5_142077636_r_count	uc010jgj.3_up_200_chr5_142077636_r_ratio	uc011dbi.2_up_200_chr5_141993727_r_count	uc011dbi.2_up_200_chr5_141993727_r_ratio	uc021yew.1_up_200_chr5_142077636_r_count	uc021yew.1_up_200_chr5_142077636_r_ratio	uc031slj.1_up_200_chr5_142000921_r_count	uc031slj.1_up_200_chr5_142000921_r_ratio	uc031slk.1_up_200_chr5_142023867_r_count	uc031slk.1_up_200_chr5_142023867_r_ratio	uc031sll.1_up_200_chr5_142065269_r_count	uc031sll.1_up_200_chr5_142065269_r_ratio	uc031slm.1_up_200_chr5_142065269_r_count	uc031slm.1_up_200_chr5_142065269_r_ratio	uc031sln.1_up_200_chr5_142065269_r_count	uc031sln.1_up_200_chr5_142065269_r_ratio	uc031slo.1_up_200_chr5_142066061_r_count	uc031slo.1_up_200_chr5_142066061_r_ratio	uc001lpv.3_up_200_chr11_535551_r_count	uc001lpv.3_up_200_chr11_535551_r_ratio	uc001lvn.2_up_200_chr11_2182440_r_count	uc001lvn.2_up_200_chr11_2182440_r_ratio	uc001lvo.1_up_200_chr11_2182440_r_count	uc001lvo.1_up_200_chr11_2182440_r_ratio	uc009ydg.1_up_200_chr11_2182219_r_count	uc009ydg.1_up_200_chr11_2182219_r_ratio	uc010qvw.2_up_200_chr11_535551_r_count	uc010qvw.2_up_200_chr11_535551_r_ratio	uc010qvx.2_up_200_chr11_535551_r_count	uc010qvx.2_up_200_chr11_535551_r_ratio	uc010qvy.2_up_200_chr11_535551_r_count	uc010qvy.2_up_200_chr11_535551_r_ratio	uc021qcd.1_up_200_chr11_2182440_r_count	uc021qcd.1_up_200_chr11_2182440_r_ratio	uc001ypj.3_up_200_chr14_105238059_r_count	uc001ypj.3_up_200_chr14_105238059_r_ratio	uc001ypk.3_up_200_chr14_105259939_r_count	uc001ypk.3_up_200_chr14_105259939_r_ratio	uc001ypl.3_up_200_chr14_105259939_r_count	uc001ypl.3_up_200_chr14_105259939_r_ratio	uc001ypm.3_up_200_chr14_105262081_r_count	uc001ypm.3_up_200_chr14_105262081_r_ratio	uc001ypn.3_up_200_chr14_105262081_r_count	uc001ypn.3_up_200_chr14_105262081_r_ratio	uc010axa.3_up_200_chr14_105260529_r_count	uc010axa.3_up_200_chr14_105260529_r_ratio	uc010tyk.2_up_200_chr14_105244016_r_count	uc010tyk.2_up_200_chr14_105244016_r_ratio	uc002bul.3_up_200_chr15_99192561_f_count	uc002bul.3_up_200_chr15_99192561_f_ratio	uc010bon.3_up_200_chr15_99192561_f_count	uc010bon.3_up_200_chr15_99192561_f_ratio	uc010boo.1_up_200_chr15_99467554_f_count	uc010boo.1_up_200_chr15_99467554_f_ratio	uc010urq.2_up_200_chr15_99192561_f_count	uc010urq.2_up_200_chr15_99192561_f_ratio	uc010urr.1_up_200_chr15_99454344_f_count	uc010urr.1_up_200_chr15_99454344_f_ratio	uc002mgd.1_up_200_chr19_7294012_r_count	uc002mgd.1_up_200_chr19_7294012_r_ratio	uc002mge.1_up_200_chr19_7294012_r_count	uc002mge.1_up_200_chr19_7294012_r_ratio	uc002mgf.3_up_200_chr19_7294012_r_count	uc002mgf.3_up_200_chr19_7294012_r_ratio
sample.bismark.cov	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	0	NA	41	0.5	2	0.5	2	0.5	7	0.5	41	0.5	41	0.5	41	0.5	2	0.5	0	NA	0	NA	0	NA	4	0.5	4	0.5	0	NA	3	0.5	0	NA	0	NA	0	NA	0	NA	0	NA	17	0.5	17	0.5	17	0.5

```




