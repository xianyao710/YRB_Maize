#Non-redundant motif indentification in Maize data set 
This YRB`_`Maize repository contains our work to implement a simple work flow for Maize CAGE data from this paper [Mejía-Guerra MK, Li W, Galeano NF, et al. Core Promoter Plasticity Between Maize Tissues and Genotypes Contrasts with Predominance of Sharp Transcription Initiation Sites. The Plant Cell. 2015;27(12):3309-3320. doi:10.1105/tpc.15.00630.](http://www.plantcell.org/content/early/2015/11/30/tpc.15.00630.short?rss=1)

#Raw data 
The orignial paper described their 4 CAGE samples: 2 for shoots tissue and 2 for roots tissue. After analyzing the tag data for these 4 samples. It is strange that shoot_1 and shoot_2 share few common tags. We thought these samples may be not good for our following motif identification since the biological duplicate should highly relavant to each other like root_1 and root_2.

#Our analysis
In order to identfiy non-redudant motifs near promoter region in Maize root tissue. We implemented our work flow which combinds cross-validation, de novo motif identification and graphical clustering.

I won't dicuss the details of implementation here which is described in my [log file](https://github.com/xianyao710/YRB_Capstone/blob/master/logs/6-14.md)

The results using original homer,tomtom parameters are weird because in theory we should expect motifs that were observed in each of the 9 training groups. These motifs should be clustered regardless of their postion in training group. At first, we suspected that it might be the parameters that affect clustering result, so we filtered homer result with e-value< 1e-20 and used tomtom threshold e-value = 0.01,0.001,0.001(false discovery rate).

![tomtom -thresh 0.01][figure]
[figure]:https://github.com/xianyao710/YRB_Maize/blob/master/figures/tomtom_0.01.png

![tomtom -thresh 0.001][figure]
[figure]:https://github.com/xianyao710/YRB_Maize/blob/master/figures/tomtom_0.001.png

![tomtom -thresh 0.0001][figure]
[figure]:https://github.com/xianyao710/YRB_Maize/blob/master/figures/tomtom_0.0001.png

No matter what parameters we used, the pipeline which proved to work find in our previous work doesn't produce convincing motif clusters. Then we suspected that the size of tags we used for homer motif identification maybe not precise. So we check the tag file and find the postion where both root_1 and root_2 have 1 or more than 1 tag here.[root_1 root_2 consensus tag position](https://github.com/xianyao710/YRB_Maize/blob/master/data/CAGE_pos_final.txt). Instead of using 50 width for TSS peak finding, we set the width as 1 bp is because these CAGE libraries don’t appear to have the same time of peak distribution than others we’ve seen (e.g. in metazoans) (cited from Taylor's email).

#latest result
I found some errors when implementing work flow and [latest result](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result) located with this directory fixing motif name error.

[raw homer result](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result/homer_motif)

[homer result converted to meme](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result/meme_motif)

[renamed meme motifs](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result/rename_motif)

After tomtom comparison using -thresh 0.0001 -evalue and clustering by networkx, three clusters were extracted (around 9 edges in each cluster) and [consensus motif](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result/Cluster_result/cluster_consensus) for each cluster were genereated.[seqLogo](https://github.com/xianyao710/YRB_Maize/tree/master/latest_result/Cluster_result/cluster_seqLogo) are available here.

