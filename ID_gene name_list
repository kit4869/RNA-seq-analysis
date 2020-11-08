if (!requireNamespace("BiocManager", quietly = TRUE)) install.packages("BiocManager")
BiocManager::install("biomaRt")

#パッケージのインストール
install.packages("dplyr")
library(dplyr)

#下記コマンドで対象種のDataset名を確認
ensembl = biomaRt::useEnsembl(biomart="ensembl")
biomaRt::listDatasets(ensembl)

#遺伝子IDと遺伝子名の対応情報を取得
mart <- biomaRt::useMart(biomart = "ENSEMBL_MART_ENSEMBL", dataset = "mmusculus_gene_ensembl", host = 'ensembl.org')
t2g <- biomaRt::getBM(attributes = c("ensembl_transcript_id", "ensembl_gene_id", "external_gene_name"), mart = mart)
t2g <- dplyr::rename(t2g, target_id = ensembl_transcript_id, ens_gene = ensembl_gene_id, ext_gene = external_gene_name)
t2g[t2g[,3] == "","ext_gene"] <- "NA"

#内容の確認
head(t2g)

#保存する
write.table(t2g, "target2gene.txt", sep = "\t", quote=F,row.names=F)
