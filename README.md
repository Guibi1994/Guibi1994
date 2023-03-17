![](images/github.png)

### Fast notes :)
#### GCP query
``` library(bigrquery)
a0_base <- bq_table_download(bq_project_query(
"project", 
` ("SQL quary")))  `
```
#### boxplot mean poitns
p <- p + stat_summary(fun.y = mean, geom = "point",
               shape = 20, size = 4, color = "turquoise") 
