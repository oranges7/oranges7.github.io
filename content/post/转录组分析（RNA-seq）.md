---
title: 转录组分析（RNA-seq）
date: 2026-01-15
share: "true"
dir: content/post
image:
tags:
categories: 转录组
description:
math: flase
---
## 上游处理
```sh
path=$(pwd)

# 创建必要的目录
mkdir -p clean_data qc_reports alignment counts


#提取fastq文件

time find raw/SRR*/*.sra | parallel -j 3 'fasterq-dump {} -O raw_data --split-3 -e 12'
time find ./raw_data -type f -name "*.fastq" | parallel -j 6 "pigz -p 6 {}"

#使用FastQC对原始数据进行质量检查
fastqc raw_data/*.fastq.gz -o qc_reports

#生成的质量报告将保存在qc_reports文件夹中，可以通过MultiQC（可选）汇总分析：
multiqc ${path}/qc_reports/*1.fastq.gz -n R1
multiqc ${path}/qc_reports/*2.fastq.gz -n R2

###在未知引物的情况下可以根据生成的质量报告进行后续引物切除###


time {
    # 使用Parallel并行处理,-f-F根据质控情况进行定义
    parallel -j 3 \
        'base=$(basename {} _1.fastq.gz);
        fastp \
            -i {} \
            -I fastq/${base}_2.fastq.gz \
            -o clean_data/${base}_R1.fastq.gz \
            -O clean_data/${base}_R2.fastq.gz \
            --thread 12 \
            ​​-f 19 \ 
            ​​-F 20' ::: fastq/*_1.fastq.gz
}
# 4. 比对到参考基因组
parallel -j 3 --progress --verbose "
  sample1={}
  base=\$(basename \${sample1} _R1.fastq.gz)
  STAR --runThreadN 12 \
    --genomeDir /mnt/hpc/home/guoyichu/reference/index/hg38/star_index \
    --readFilesIn \${sample1} clean_data/\${base}_R2.fastq.gz \
    --readFilesCommand zcat \
    --outFileNamePrefix alignment/\${base}_ \
    --outSAMtype BAM Unsorted
    
  samtools sort -@ 24 -m 4G \
    -o alignment/\${base}_sorted.bam \
    alignment/\${base}_Aligned.out.bam

  # 清理中间文件
  rm alignment/\${base}_Aligned.out.bam
" ::: clean_data/*_R1.fastq.gz
# 5. 生成基因计数矩阵
time featureCounts -T 24 -p -a GCF_000001405.40_GRCh38.p14_genomic.gtf -o counts/gene_counts.txt alignment/*_sorted.bam
```

## 下游处理

### 数据导入与质控

#### 从上游处理导入

```sh
setwd("设置工作目录")
data <- read.delim("gene_counts.txt", 
                   header = TRUE,       # 第一行作为表头
                   sep = "\t",          # 指定分隔符为 tab
                   comment.char = "#")  # 忽略以 # 开头的行
#设置行名
rownames(data) <- data$Geneid
exp_mat <- data[, -c(1,2, 3, 4, 5, 6)]
colnames(exp_mat) <- gsub("alignment.|_Aligned.sortedByCoord.out.bam", "", colnames(exp_mat))
exp_mat_filtered <- exp_mat %>%
  # 过滤低表达基因：每行至少有X个样本的表达值大于Y
  filter(rowSums(. > 5) >= ncol(.) * 0.5) %>%  # 举例：表达值>1的样本数要占总样本数20%以上
  # 过滤低方差基因
  filter(apply(., 1, var) > quantile(apply(., 1, var), 0.1))  # 保留方差前90%的基因
#导入metadata分组信息
meta_P999 <- read.csv("",row.names = 1)

```
#### 从NCBI下载


### 差异分析

### 富集分析


### 机器学习
