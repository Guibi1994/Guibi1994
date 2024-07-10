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
#### Save plots in googledrive
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
#### Fast Barplots
```
univar_plot <- function(data,variable) {
  ncolors = data %>%
    summarise(ncolors = n_distinct({{variable}})) %>%
    pull(ncolors)
  
  data %>% 
    group_by({{variable}}) %>% 
    summarise(n = n()) %>%
    mutate(tot= sum(n),
           pp = 100*round(n/tot,3),
           my_label = paste0(n, " (",pp,"%)"),
           text_color = ifelse(pp>1.5,"white","grey20"),
           text_position = ifelse(pp>1.5,(n/2),quantile(n,probs = 0.3)),
           text_angle = ifelse(pp>10,0,270)) %>% 
    # Plot
    ggplot(aes(n, {{variable}},
               group = {{variable}},
               fill = {{variable}})) +
    scale_fill_manual(values = c(my_colors[1:ncolors]))+
    geom_bar(stat = "identity", alpha = .8)+
    geom_text(aes(text_position,{{variable}}, label = my_label,
                  family = "serif",color = text_color, 
                  angle = text_angle),size = 3)+
    scale_color_identity()+
    #Theme
    my_theme
}
bivar_plot <- function(data, var1,var2) {
  data %>% 
    group_by({{var1}}, {{var2}}) %>% 
    summarise(n = n()) %>% 
    arrange(desc({{var2}})) %>% 
    group_by({{var1}}) %>% 
    mutate(tot = sum(n),
           pp = round(n/tot,3),
           text_position = ((cumsum(pp))-pp)+(pp/2),
           my_label = paste0(n, "  (",100*pp,"%)"),
           text_color = ifelse(pp>.02,"white","grey"),
           text_angle = ifelse(pp>.1,0,-90)) %>% 
    # Plot
    ggplot(aes(pp,{{var1}},fill = {{var2}}))+
    geom_bar(stat = "identity")+
    scale_fill_manual(values = c(my_colors))+
    geom_text(aes(text_position,{{var1}}, label = my_label,
                  family = "serif", color = text_color, angle = text_angle),
              size = 3)+
    scale_color_identity()+
    my_theme2
}
```
