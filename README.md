本基因集库来自于<https://yulab-smu.top/gson-files/>，由于没有WikiPathways的库，所以在Y叔的基础上进行了修改，并且使用最新的数据，本版的更新时期是2022年11月21日。

`gson`文件格式是在CRAN R包[gson](https://CRAN.R-project.org/package=gson)中提取的。

此格式旨在存储具有相关信息（例如基因集名称、版本、物种等）的基因集。

[gson](https://CRAN.R-project.org/package=gson) 包提供了一组用于读取、写入和处理`gson`文件的实用程序。

以下是以`gson`格式存储的基因集库：

| Gene Set          | Terms | Gene Coverage | Species      | Version                         | URL                                                                                                                                           |
|:----------|----------:|----------:|:----------|:----------|:----------------|
| Gene Ontology;ALL | 22741 |         20757 | Homo sapiens | 2023-07-27                      | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/GO_ALL_human.gson)       |
| Gene Ontology;BP  | 15709 |         18870 | Homo sapiens | 2023-07-27                      | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/GO_BP_human.gson)        |
| Gene Ontology;CC  |  1977 |         19886 | Homo sapiens | 2023-07-27                      | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/GO_CC_human.gson)        |
| Gene Ontology;MF  |  5055 |         18496 | Homo sapiens | 2023-07-27                      | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/GO_MF_human.gson)        |
| KEGG              |   356 |          8644 | hsa          | Release 108.0+/12-23, Dec 23    | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/KEGG_human.gson)         |
| KEGG              |   193 |           855 | hsa          | Release 108.0+/12-23, Dec 23    | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/MKEGG_human.gson)        |
| reactome pathway  |  2602 |         11009 | human        | Version: 86; Source date: 19635 | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/Reactome_human.gson)     |
| WikiPathways      |   845 |          8389 | Homo sapiens | WikiPathways_20231210           | [<img src="https://swcyo.github.io/gson-file/img/download-solid.svg" width="30"/>](https://swcyo.github.io/gson-file/WikiPathways_human.gson) |

用户可以下载该文件并将其用作[clusterProfiler](http://bioconductor.org/packages/clusterProfiler)包中的背景注释，用以运行富集分析。

-   获取在线gson的代码如下：

```         
    # GO
    library(clusterProfiler)
    library(org.Hs.eg.db)
    library(gson)
    gson_BP_human <- gson_GO(OrgDb = org.Hs.eg.db, keytype = 'ENTREZID', ont = "BP")
    gson_MF_human <- gson_GO(OrgDb = org.Hs.eg.db, keytype = 'ENTREZID', ont = "MF")
    gson_CC_human <- gson_GO(OrgDb = org.Hs.eg.db, keytype = 'ENTREZID', ont = "CC")
    gson_ALL_human <- gson_GO(OrgDb = org.Hs.eg.db, keytype = 'ENTREZID', ont = "ALL")
    write.gson(gson_BP_human, file = "GO_BP_human.gson")
    write.gson(gson_MF_human, file = "GO_MF_human.gson")
    write.gson(gson_CC_human, file = "GO_CC_human.gson")
    write.gson(gson_ALL_human, file = "GO_ALL_human.gson")

    # KEGG
    KEGG_human <- gson_KEGG(species = "hsa", KEGG_Type="KEGG", keyType="kegg") 
    MKEGG_human <- gson_KEGG(species = "hsa", KEGG_Type="MKEGG", keyType="kegg") 
    write.gson(KEGG_human, file = "KEGG_human.gson")
    write.gson(MKEGG_human, file = "MKEGG_human.gson")

    # WikiPathways
    WikiPathways_human <- gson_WP("Homo sapiens") 
    write.gson(WikiPathways_human, file = "WikiPathways_human.gson")

    # Reactome
    library(ReactomePA)
    Reactome_human <- gson_Reactome(organism = "human")
    write.gson(Reactome_human, file = "Reactome_human.gson")
```
