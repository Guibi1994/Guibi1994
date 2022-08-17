# Guibor Camargo Salamanca

Researcher at @EconUrosario, Data Scientist at @Cívico

### Notas rápidas

`library(bigrquery)`

`a0_base <- bq_table_download(bq_project_query(`

`"atlas-323415", # Proyececto`

`` ("SELECT  * FROM `atlas-323415.cooked_data.CT01_customer_total`"))) # Consulta ``
