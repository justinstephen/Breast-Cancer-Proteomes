Breast Cancer Proteomes
================

First looking at the cancer samples data:

``` r
samples <- as.data.frame(read.csv("./data/clinical_data_breast_cancer.csv", header = TRUE))
```

Looking some of the summary data

``` r
dim(samples)
```

    ## [1] 105  30

``` r
summary(samples)
```

    ##      Complete.TCGA.ID    Gender    Age.at.Initial.Pathologic.Diagnosis
    ##  TCGA-A2-A0CM: 1      FEMALE:103   Min.   :30.00                      
    ##  TCGA-A2-A0D0: 1      MALE  :  2   1st Qu.:49.00                      
    ##  TCGA-A2-A0D1: 1                   Median :58.00                      
    ##  TCGA-A2-A0D2: 1                   Mean   :58.69                      
    ##  TCGA-A2-A0EQ: 1                   3rd Qu.:67.00                      
    ##  TCGA-A2-A0EV: 1                   Max.   :88.00                      
    ##  (Other)     :99                                                      
    ##          ER.Status     PR.Status  HER2.Final.Status Tumor  
    ##  Indeterminate: 1   Negative:51   Equivocal: 1      T1:15  
    ##  Negative     :36   Positive:54   Negative :77      T2:65  
    ##  Positive     :68                 Positive :27      T3:19  
    ##                                                     T4: 6  
    ##                                                            
    ##                                                            
    ##                                                            
    ##  Tumor..T1.Coded Node       Node.Coded Metastasis Metastasis.Coded
    ##  T_Other:90      N0:53   Negative:53   M0:103     Negative:103    
    ##  T1     :15      N1:29   Positive:52   M1:  2     Positive:  2    
    ##                  N2:14                                            
    ##                  N3: 9                                            
    ##                                                                   
    ##                                                                   
    ##                                                                   
    ##       AJCC.Stage      Converted.Stage  Survival.Data.Form   Vital.Status
    ##  Stage IIA :30   No_Conversion:41     enrollment:58       DECEASED:11   
    ##  Stage IIB :23   Stage I      : 8     followup  :47       LIVING  :94   
    ##  Stage IIIA:12   Stage IIA    :28                                       
    ##  Stage II  :11   Stage IIB    :16                                       
    ##  Stage IA  : 7   Stage IIIA   : 6                                       
    ##  Stage IIIB: 6   Stage IIIB   : 2                                       
    ##  (Other)   :16   Stage IIIC   : 4                                       
    ##  Days.to.Date.of.Last.Contact Days.to.date.of.Death    OS.event     
    ##  Min.   :   0.0               Min.   : 160.0        Min.   :0.0000  
    ##  1st Qu.: 240.0               1st Qu.: 947.5        1st Qu.:0.0000  
    ##  Median : 643.0               Median :1364.0        Median :0.0000  
    ##  Mean   : 788.4               Mean   :1254.5        Mean   :0.1048  
    ##  3rd Qu.:1288.0               3rd Qu.:1627.5        3rd Qu.:0.0000  
    ##  Max.   :2850.0               Max.   :2483.0        Max.   :1.0000  
    ##                               NA's   :94                            
    ##     OS.Time               PAM50.mRNA SigClust.Unsupervised.mRNA
    ##  Min.   :   0.0   Basal-like   :25   Min.   :-12.000           
    ##  1st Qu.: 240.0   HER2-enriched:18   1st Qu.: -6.000           
    ##  Median : 665.0   Luminal A    :29   Median : -5.000           
    ##  Mean   : 817.6   Luminal B    :33   Mean   : -4.886           
    ##  3rd Qu.:1305.0                      3rd Qu.: -3.000           
    ##  Max.   :2850.0                      Max.   :  0.000           
    ##                                                                
    ##  SigClust.Intrinsic.mRNA miRNA.Clusters methylation.Clusters RPPA.Clusters
    ##  Min.   :-13.000         Min.   :1      Min.   :1.000        Basal :29    
    ##  1st Qu.:-12.000         1st Qu.:3      1st Qu.:2.000        Her2  :18    
    ##  Median : -6.000         Median :4      Median :4.000        LumA  : 9    
    ##  Mean   : -7.181         Mean   :4      Mean   :3.343        LumA/B:22    
    ##  3rd Qu.: -2.000         3rd Qu.:5      3rd Qu.:4.000        ReacI :11    
    ##  Max.   :  0.000         Max.   :7      Max.   :5.000        ReacII:13    
    ##                                                              X     : 3    
    ##   CN.Clusters   Integrated.Clusters..with.PAM50.
    ##  Min.   :1.00   Min.   :1.000                   
    ##  1st Qu.:1.00   1st Qu.:2.000                   
    ##  Median :3.00   Median :3.000                   
    ##  Mean   :2.59   Mean   :2.743                   
    ##  3rd Qu.:3.00   3rd Qu.:4.000                   
    ##  Max.   :5.00   Max.   :4.000                   
    ##                                                 
    ##  Integrated.Clusters..no.exp. Integrated.Clusters..unsup.exp.
    ##  Min.   :1.000                Min.   :1.000                  
    ##  1st Qu.:1.000                1st Qu.:1.000                  
    ##  Median :2.000                Median :2.000                  
    ##  Mean   :1.981                Mean   :2.352                  
    ##  3rd Qu.:3.000                3rd Qu.:3.000                  
    ##  Max.   :4.000                Max.   :5.000                  
    ## 

There are 105 samples with 30 different features. 
* **Complete.TCGA.ID**: The ID of the sample 
* **Gender**:
* **Age.at.Initial.Pathologic.Diagnosis**:
* **ER.Status**: Estrogen Receptor Status
* **PR.Status**: Progesterone Receptor Status
* **HER2.Final.Status**: Human Epidermal Growth Factor-2
* **Tumor**: Factors of the size of the Tumor (T1, T2, T3, T4)
* **Tumor..T1.Coded**: Coded for just T1 tumors
* **Node**: Factor of how far the cancer has spread to nearby nodes with N0 indicating no spread. (N0, N1, N2, N4)
* **Node.Coded**: Negative indicates N0 (no spread), Positive indicates N1-N3.
* **Metastasis**: Factor indicating if cancer has spread to other parts of the body. M0 indicates no distant metastatis, M1 indicates Distant metastasis
* **Metastasis.Coded**: Negative indicates M0, Positive indicates M1
* **AJCC.Stage**: Factors of the stage of the concers. This is determined by combining the T, N, and M categories.
* **Converted.Stage**
* **Survival.Data.Form**: 
* **Vital.Status**: 
* **Days.to.Date.of.Last.Contact**
* **Days.to.date.of.Death**
* **OS.event**
* **S.Time**
* **PAM50.mRNA**
* **SigClust.Unsupervised.mRNA**
* **SigClust.Intrinsic.mRNA**
* **miRNA.Clusters**
* **methylation.Clusters**
* **RPPA.Clusters**
* **CN.Clusters**
* **Integrated.Clusters..with.PAM50.**
* **Integrated.Clusters..no.exp.**
* **Integrated.Clusters..unsup.exp.**
``` r
ggplot(samples, aes(x = Age.at.Initial.Pathologic.Diagnosis)) +
  geom_histogram(colour = "darkgreen", fill = "white", binwidth = 3)
```

![](Breast_Cancer_Proteomes_files/figure-markdown_github/Age-1.png)

``` r
plot_ER <- ggplot(samples, aes(x = ER.Status)) +
  geom_bar()
plot_PR <- ggplot(samples, aes(x = PR.Status)) +
  geom_bar()

grid.arrange(plot_ER, plot_PR, ncol=2)
```

![](Breast_Cancer_Proteomes_files/figure-markdown_github/Status-1.png)

``` r
plot_Tumor <- ggplot(samples, aes(x = Tumor)) +
  geom_bar()
plot_Node <- ggplot(samples, aes(x = Node)) +
  geom_bar()
plot_Metastasis <- ggplot(samples, aes(x = Metastasis)) +
  geom_bar()

grid.arrange(plot_Tumor, plot_Node, plot_Metastasis, ncol=3)
```

![](Breast_Cancer_Proteomes_files/figure-markdown_github/Types-1.png)
=======
