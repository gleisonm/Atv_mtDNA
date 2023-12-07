#  _Mesonauta festivus_ - mtDNA

![GitHub language count](FASTA)
![GitHub forks](https://img.shields.io/github/forks/iuricode/README-template?style=for-the-badge)
![Bitbucket open issues](https://img.shields.io/bitbucket/issues/iuricode/README-template?style=for-the-badge)
![Bitbucket open pull requests](https://img.shields.io/bitbucket/pr-raw/iuricode/README-template?style=for-the-badge)

<img src="mtDNA.png" alt="mtDNA">

> Projeto de montagem e análise do DNA mitocondrial do peixe _Mesonauta Festivus_.

### Ajustes e melhorias

O projeto ainda está em desenvolvimento e as próximas atualizações serão voltadas nas seguintes tarefas:

- [x] Montagem
- [x] Anotação
- [x] tRNA scan
- [x] RCSU
- [x] Regiões secundárias D-loop
- [x] Árvore filogenética

## 💻 Softwares utilizados

- NOVOPlasty
- Mitoz
- tRNAscan-SE
- BLASTn
- Mitoannotator
- Nextflow

## 🚀 Metodologia


Para a moontagem do mtDNA tilizamos as reads de acesso [ERX10239209](https://www.ncbi.nlm.nih.gov/sra/ERX10239209)
Como seed do NOVOPlasty utilizamos o mtDNA de acesso [NC_033550.1](https://www.ncbi.nlm.nih.gov/nuccore/NC_033550.1/)

A parte de montagem, anotação e tRNAs está automatizada em um pipline em desenvolvimento em nextflow:
[mitomine - NextFlow](https://github.com/gleisonm/mitomine.git)

### Montagem:

NOVOPlasty
```
Project:
-----------------------
Project name          = ${prefix}_${run}
Type                  = mito
Genome Range          = 13000-18000
K-mer                 = 33
Max memory            = 120
Extended log          = 0
Save assembled reads  = no
Seed Input            = $seed
Extend seed directly  = no
Reference sequence    =
Variance detection    =
Chloroplast sequence  =

Dataset 1:
-----------------------
Read Length           = 151
Insert size           = 525
Platform              = illumina
Single/Paired         = PE
Combined reads        =
Forward reads         = /data/home/gleison.azevedo/ciclideos/data/raw/${reads[0]}
Reverse reads         = /data/home/gleison.azevedo/ciclideos/data/raw/${reads[1]}
Store Hash            =

Heteroplasmy:
-----------------------
MAF                   =
HP exclude list       =
PCR-free              =

Optional:
-----------------------
Insert size auto      = yes
Use Quality Scores    = no
Reduce ambigious N's  =
Output path           =
```
> Este processo é repetido utilizando o output como seed para afim de polir a montagem
```
Project:
-----------------------
Project name          = ${prefix}_polish
Type                  = mito
Genome Range          = 13000-18000
K-mer                 = 33
Max memory            = 120
Extended log          = 0
Save assembled reads  = no
Seed Input            = $seed
Extend seed directly  = no
Reference sequence    =
Variance detection    =
Chloroplast sequence  =

Dataset 1:
-----------------------
Read Length           = 151
Insert size           = 525
Platform              = illumina
Single/Paired         = PE
Combined reads        =
Forward reads         = /data/home/gleison.azevedo/ciclideos/data/raw/$fastq1
Reverse reads         = /data/home/gleison.azevedo/ciclideos/data/raw/$fastq2
Store Hash            =

Heteroplasmy:
-----------------------
MAF                   =
HP exclude list       =
PCR-free              =

Optional:
-----------------------
Insert size auto      = yes
Use Quality Scores    = no
Reduce ambigious N's  =
Output path           =
```
> Outputs:
> <novoplastyout>

Mitoz
```
fastq1=/storages/acari/gleison.azevedo/ciclideos/data/raw/ERR10789898_Illumina_NovaSeq_6000_paired_end_sequencing_1.fastq.gz
fastq2=/storages/acari/gleison.azevedo/ciclideos/data/raw/ERR10789898_Illumina_NovaSeq_6000_paired_end_sequencing_2.fastq.gz

mitoz all  \
--outprefix Mfestivus_ERR10789898 \
--thread_number 8 \
--clade Chordata \
--genetic_code 2 \
--species_name "Mesonauta festivus" \
--fq1 $fastq1 \
--fq2 $fastq2 \
--fastq_read_length 151 \
--data_size_for_mt_assembly 3,0 \
--assembler megahit \
--kmers_megahit 59 79 99 119 141 \
--memory 80 \
--requiring_taxa Chordata
```
> Outputs:
> <mitoz out>

As mitocondrias foram alinhadas utilizando BLAST e obtiveram .....

### Anotação:

As mitocôndrias foram anotadas no [MitoAnnotator](http://mitofish.aori.u-tokyo.ac.jp/annotation/input/)
> Outputs:
> <MitoAnnotator out>

### tRNAscan:

Os tRNAs foram obtidos pelo mitoz e plotados pelo programa [tRNAscan-SE](http://lowelab.ucsc.edu/tRNAscan-SE/)

#### Outputs:
<img src="drwtrna123814.gif" alt="tRNA">
<img src="drwtrna123845.gif" alt="tRNA">
<img src="drwtrna123876.gif" alt="tRNA">
<img src="drwtrna123906.gif" alt="tRNA">
<img src="drwtrna123938.gif" alt="tRNA">
<img src="drwtrna123969.gif" alt="tRNA">
<img src="drwtrna124037.gif" alt="tRNA">
<img src="drwtrna124007.gif" alt="tRNA">
<img src="drwtrna124097.gif" alt="tRNA">
<img src="drwtrna124067.gif" alt="tRNA">
<img src="drwtrna124127.gif" alt="tRNA">
<img src="drwtrna124157.gif" alt="tRNA">
<img src="drwtrna124187.gif" alt="tRNA">
<img src="drwtrna124217.gif" alt="tRNA">
<img src="drwtrna124247.gif" alt="tRNA">
<img src="drwtrna124279.gif" alt="tRNA">
<img src="drwtrna124309.gif" alt="tRNA">
<img src="drwtrna124340.gif" alt="tRNA">
<img src="drwtrna124371.gif" alt="tRNA">
<img src="drwtrna124433.gif" alt="tRNA">
<img src="drwtrna124468.gif" alt="tRNA">
```
Sequence                                		tRNA	Bounds	tRNA	Anti	Intron Bounds	Inf	      
Name                                    	tRNA #	Begin	End	Type	Codon	Begin	End	Score	Note
--------                                	------	-----	------	----	-----	-----	----	------	------
k141_742411_trnK_uuu__len_75__308_383_- 	1	1 	75	Lys	TTT	0	0	109.1	
k141_742411_trnD_guc__len_73__1079_1152_-	1	1 	73	Asp	GTC	0	0	97.5	
k141_742411_trnS_uga__len_71__1157_1228_	1	1 	71	Ser	TGA	0	0	107.4	
k141_742411_trnY_gua__len_70__2806_2876_	1	1 	70	Tyr	GTA	0	0	104.8	
k141_742411_trnC_gca__len_65__2876_2941_	1	1 	65	Cys	GCA	0	0	83.1	
k141_742411_trnN_guu__len_73__2977_3050_	1	1 	73	Asn	GTT	0	0	110.2	
k141_742411_trnA_ugc__len_69__3051_3120_	1	1 	69	Ala	TGC	0	0	106.5	
k141_742411_trnW_uca__len_72__3121_3193_-	1	1 	72	Trp	TCA	0	0	97.1	
k141_742411_trnM_cau__len_69__4239_4308_-	1	1 	69	Met	CAT	0	0	116.9	
k141_742411_trnQ_uug__len_71__4307_4378_	1	1 	71	Gln	TTG	0	0	107.2	
k141_742411_trnI_gau__len_70__4377_4447_-	1	1 	70	Ile	GAT	0	0	100.7	
k141_742411_trnL_uaa__len_74__5425_5499_-	1	1 	74	Leu	TAA	0	0	114.7	
k141_742411_trnV_uac__len_72__7189_7261_-	1	1 	72	Val	TAC	0	0	96.6	
k141_742411_trnF_gaa__len_69__8212_8281_-	1	1 	69	Phe	GAA	0	0	91.9	
k141_742411_trnP_ugg__len_70__9138_9208_	1	1 	70	Pro	TGG	0	0	100.6	
k141_742411_trnT_ugu__len_71__9207_9278_-	1	1 	71	Thr	TGT	0	0	84.2	
k141_742411_trnE_uuc__len_69__10427_10496_	1	1 	69	Glu	TTC	0	0	97.7	
k141_742411_trnL_uag__len_73__12853_12926_-	1	1 	73	Leu	TAG	0	0	114.3	
k141_742411_trnS_gcu__len_67__12930_12997_-	1	1 	67	Ser	GCT	0	0	70.7	No D-arm
k141_742411_trnH_gug__len_69__12997_13066_-	1	1 	69	His	GTG	0	0	105.4	
k141_742411_trnR_ucg__len_69__14737_14806_-	1	1 	69	Arg	TCG	0	0	92.6	
k141_742411_trnG_ucc__len_72__15155_15227_-	1	1 	72	Gly	TCC	0	0	104.6	
```

### Árvore Filogenética:

Os tRNAs foram obtidos pelo mitoz e plotados pelo programa [tRNAscan-SE](http://lowelab.ucsc.edu/tRNAscan-SE/)



### RSCU:

O RSCU foi calculado pelo [RSCURS](https://www.lirmm.fr/~rivals/rscu/)

### Regiões secundárias: D-loop


## ☕ Usando <nome_do_projeto>

Para usar <nome_do_projeto>, siga estas etapas:

```
<exemplo_de_uso>
```

Adicione comandos de execução e exemplos que você acha que os usuários acharão úteis. Fornece uma referência de opções para pontos de bônus!

## 📫 Contribuindo para <nome_do_projeto>

Para contribuir com <nome_do_projeto>, siga estas etapas:

1. Bifurque este repositório.
2. Crie um branch: `git checkout -b <nome_branch>`.
3. Faça suas alterações e confirme-as: `git commit -m '<mensagem_commit>'`
4. Envie para o branch original: `git push origin <nome_do_projeto> / <local>`
5. Crie a solicitação de pull.

Como alternativa, consulte a documentação do GitHub em [como criar uma solicitação pull](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request).

## 🤝 Colaboradores

Agradecemos às seguintes pessoas que contribuíram para este projeto:

<table>
  <tr>
    <td align="center">
      <a href="#" title="defina o titulo do link">
        <img src="https://avatars3.githubusercontent.com/u/31936044" width="100px;" alt="Foto do Iuri Silva no GitHub"/><br>
        <sub>
          <b>Iuri Silva</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="#" title="defina o titulo do link">
        <img src="https://s2.glbimg.com/FUcw2usZfSTL6yCCGj3L3v3SpJ8=/smart/e.glbimg.com/og/ed/f/original/2019/04/25/zuckerberg_podcast.jpg" width="100px;" alt="Foto do Mark Zuckerberg"/><br>
        <sub>
          <b>Mark Zuckerberg</b>
        </sub>
      </a>
    </td>
    <td align="center">
      <a href="#" title="defina o titulo do link">
        <img src="https://miro.medium.com/max/360/0*1SkS3mSorArvY9kS.jpg" width="100px;" alt="Foto do Steve Jobs"/><br>
        <sub>
          <b>Steve Jobs</b>
        </sub>
      </a>
    </td>
  </tr>
</table>

## 😄 Seja um dos contribuidores

Quer fazer parte desse projeto? Clique [AQUI](CONTRIBUTING.md) e leia como contribuir.

## 📝 Licença

Esse projeto está sob licença. Veja o arquivo [LICENÇA](LICENSE.md) para mais detalhes.
