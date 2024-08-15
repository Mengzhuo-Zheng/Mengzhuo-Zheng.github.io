---
scMetabolism 使用指南
---

## 01 安装及数据导入
```R
install.packages(c("devtools", "data.table", "wesanderson", "Seurat", "devtools", "AUCell", "GSEABase", "GSVA", "ggplot2","rsvd"))
devtools::install_github("YosefLab/VISION@v2.1.0") #Please note that the version would be v2.1.0
devtools::install_github("wu-yc/scMetabolism")
library(scMetabolism)
library(ggplot2)
library(rsvd)
load(file = "pbmc_demo.rda")
```

## 02 利用 Seurat 量化单细胞代谢水平
```R
countexp.Seurat<-sc.metabolism.Seurat(obj = countexp.Seurat, 
                  method = "AUCell", 
                  imputation = F, 
                  ncores = 2, 
                  metabolism.type = "KEGG")

```
- `obj`: 单细胞Seurat对象
- `method`：可选择VISION（默认）, AUCell, ssgsea, gsva.
- `imputation`：允许用户选择是否在代谢评分前对其数据进行估算.
- `ncores`：并行计算线程数.
- `metabolism.type`：可选择 `KEGG`（85条通路）或 `REACTOME`（82条通路）

## 03 提取代谢评分
```R
metabolism.matrix <- countexp.Seurat@assays$METABOLISM$score
```
## 04 可视化
### 04-1 Dimplot点图：特定pathway的umap降维可视化
```R
DimPlot.metabolism(obj = countexp.Seurat, 
          pathway = "Glycolysis / Gluconeogenesis", 
          dimention.reduction.type = "umap", 
          dimention.reduction.run = F, 
          size = 1)
```
![](./scmetabolism_dimplot)
