**DE Fundamentals Assignment**

**Identified Problems**  
1\. The company's analytical strategy is not in good shape.  
2\. Reporting is delayed, affecting stakeholder decision-making.  
3\. Customer service is being negatively impacted.

A full data engineering lifecycle is proposed to improve customer service and make data readily  
available for further insights that can support business growth.

![][image1]

**Collection**  
![][image2]  
**Social Media**: Largely unstructured data, consisting mainly of customer posts or tweets.  
**Call Center Logs**: A combination of structured and unstructured data. Structured data may include agent\_id, call\_id, call\_duration, and call\_outcome, while unstructured data may include call recordings.  
**SMS**: Unstructured customer message data.  
**Website Form**: Structured data collected through the form fields.

**Ingestion.**  
The primary business requirement is reporting and analytics to support informed decision-making. Therefore, batch processing will be used to move data from the various sources into the analytical environment.

Given the volume of data being generated, incremental loading will be used so that only newly generated data is processed during each run.

* **Social Media**: API ingestion from the source.  
* **Call Center Logs**: File uploads containing call details in CSV format and call audio files.  
* **SMS**: API ingestion from the source.  
* **Website Form**: CSV file uploads from the source.

**Storage**  
The system is being designed as an OLAP environment to support analysis and decision making. A data lake will be used as the preferred storage layer because it can accommodate both structured and unstructured data.  
The Extract–Load–Transform (ELT) approach will be used. Raw data will first be loaded and preserved before transformation. This provides flexibility because analytical requirements may change over time. The data lake also supports schema-on-read.

**Transformation**.  
Transformation will be performed after the raw data has been loaded. The cleaning process will include:  
• Removing duplicate records.  
• Standardizing formats such as phone numbers, date/time, and channel.  
• Trimming unnecessary whitespaces.  
• Separating invalid entries from valid data.

After cleaning, complaints will be categorized using keyword-based classification. Keywords will be used to group complaints into defined categories such as Network Issues and Billing Issues.  
The transformed data will then be stored in transformed tables and made ready for use

**Serving**  
One of Beejan Technologies’ major challenges is the slow process of gathering reports.  
To address this, the transformed and aggregated data will be made available to users for analysis. Data analysts will connect visualization tools such as Power BI or Tableau to the transformed data. The resulting dashboards will allow end users to access the required insights without having to manually gather the underlying data.

**Orchestration and Monitoring**  
The pipeline execution frequency will depend on the management Service Level Agreement (SLA) for reporting. For a dashboard providing insights into customer complaints, an hourly pipeline run may be required so that updated data is available for serving. Where reporting is only required monthly, a daily end-of-day pipeline run would be sufficient. Pipeline failures will be detected through monitoring and failure alerts. Alerts will notify the responsible team when a pipeline failure occurs so that the issue can be addressed immediately. 

**DataOps**  
The complete pipeline is expected to run within a virtual machine, most likely in a Linux environment. The pipeline code developed in the development environment will be moved to the production environment as part of the deployment process. This ensures that the developed data engineering pipeline is made available for execution in production. 

![][image3]