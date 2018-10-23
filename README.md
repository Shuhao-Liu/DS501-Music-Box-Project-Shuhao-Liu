# DS501-Music-Box-Project-Shuhao-Liu
The goal of the project is to predict the user churn rate. This readme file summarizes the workflow and acts as an index. 
The raw data were downloaded and processed with commands in 

0_create_data_folders
1_download_data.ipynb
2_unpack_and_clean_files

Databricks.com in combination with Amazon Web Service (AWS) was used to do the analysis. Since Databricks can only hold single file up to 2gb, the all_play_log is too large (>10gb) to upload. Bash command:
split -l 22000000 all_play_log 
was used to split the all_play_log to 7 files. All files are less than 2gb in size. 
