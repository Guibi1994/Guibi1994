![](images/github.png)

### Fast notes :)
#### GCP query
``` library(bigrquery)
a0_base <- bq_table_download(bq_project_query(
"project", 
` ("SQL quary")))  `
```
#### boxplot mean poitns
```
p <- p + stat_summary(fun.y = mean, geom = "point",
               shape = 20, size = 4, color = "turquoise") 
```
### Save plots in googledrive
```
ggdrive_save <- function(
    plot,
    drive_location,
    name,w =5,h=5) {
  # Description: This funtion exports an image to drive
  
  # a. Local saving
  ggplot2::ggsave(
    plot = plot,
    filename = name,
    width = w,
    height = h)
  # b. Drive saving
  googledrive::drive_upload(
    media = name,
    path = paste0(drive_location,"/",name),
    overwrite = T)
  # c. Removign local file
  file.remove(name)
}
```
