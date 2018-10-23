# DS501-Music-Box-Project-Shuhao-Liu
The goal of the project is to predict the user churn rate. This readme file summarizes the workflow and acts as an index. 
For some files both html and ipynb were uploaded for better viewing results.
The raw data were downloaded and processed with commands in 

0_create_data_folders
1_download_data.ipynb
2_unpack_and_clean_files

Databricks.com in combination with Amazon Web Service (AWS) was used to do the analysis. Since Databricks can only hold single file up to 2gb, the all_play_log is too large (>10gb) to upload. Bash command:

split -l 22000000 all_play_log 

was used to split the all_play_log to 7 files (each file has 22000000 lines except the last one). All files are less than 2gb in size. Downsampling was not applied in this case and all data were used for analysis. 

uid_count was also created with the first part of 

3_bot user removal and event table creation.ipynb

Then all data files:

all_down_log
all_search_log
all_play_log_split (1 to 7)
uid_count.csv

were uploaded to Databricks File System (DBFS). The data are acutally stored in S3 bucket by AWS and DFBS is a layer of interface. Note that before uploading, first line (some sort of code) of all_search_log was deleted and in first line of uid_count, the ' ' uid was changed to '-1' for consistency.

Rest of process can be seen in those files:

3_bot user removal and event table creation.ipynb
4_feature_label_generation_with_spark.ipynb
5_train_model_spark_ml.ipynb

Extra notes regarding AWS EC2 usage:

Databricks charges AWS EC2 usage by Databricks unit (DBU) in addition to AWS EC2 cost. During the cluster creation, I explored the possiblity of EC2 unit combination. For general purpose, I used a cluster with an on-demand m5.large as driver (cheapest option, 8gb memory, 2 cores) and an on-spot m4.xlarge (16gb memory, 4 cores) as worker with 40% percent of on-demand instance price bidding (since according to AWS chart, m4.xlarge usually is 70% off for on-spot price, and not highly demanded).

However this cluster was not enought for modelling all those data. In the modelling stage, a cluster with one on-demand r4.4xlarge (122 gb memory, 16cores) driver and 6 on-spot m4.2xlarge (32gb 8cores) workers with 88% percent of on-demand instance price bidding was used.

Total cost for the project was less than $8 total. Almost all cost was from EC2. Storage cost less than $0.2. 
