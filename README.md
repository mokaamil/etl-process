# ETL Tools
Pentaho Data integration (PDI) is part of the Pentaho suite that consists of sets of software which mainly handles data flow design. It provides Extract, Transform, and Load (ETL) capabilities that includes capturing, cleansing, and storing data. With the help of its interactive graphical interface, PDI is not only easy to use but also offers powerful components for gathering data from multiple sources, blend data into a single location, and achieve a uniform data format. 

## ETL process overview 
1. Requirements gathering process includes wireframe (prototype) or source system (live interface) interpretation, discussion with stakeholders (System Developer, Business Analysts, SME’s, Business Intelligence, etc.)
2. Study important aspect of the project to construct Data Model that suits business rule
3. Compose ETL documentation such as source-to-target mapping, table list to be created and data modelling
4. Develop database structure for storage that consists of staging tables, main facts and dimensions (lookup & transactional)
5. Design PDI transformation/jobs also known as data pipeline to handle data transformation process
6. Test ETL data flow component and data checking
7. Deployment

## Example of ETL process in a project
1) Requirements Gathering
    - Fundamental understanding regarding business process and project expected outcome are being explored by getting as much input from the related stakeholders that includes but not limited to: -  
        - Discover how frontend interface being develop – To record what data scope that are available in the OLTP system and which one involve.
        - Understand the integration part from OLTP platform to OLAP component in terms of how the data is being flow, what type of data is being passed (flat file,  csv, json, etc.).
        - Clarify the OLTP system’s essential aspect with Business Analyst and SME to further outline perspective such as data availability, data correlation, and needs in reporting. This will answer the purpose of data.
    
2)	Data Dimensional Modelling
    - Define table structure, variable included, and rules for relationship between table.
    - Choose schema that fits OLAP requirements such as star or snowflake schema.
    - Finalize data rule for data elimination.

3)	Database Management
    - Build database structure that includes table correlation.
    - Documents table list that covers attributes, key relations, constraints, and description.

4)	Develop ETL transformation jobs
    - Design ETL process in data pipeline (Further example in Demonstration part) 
    - Analyze data by data profiling to understand data structure, quality, content, and relationship of source data.
    - Involves processing data file from integration such as retrieving data, combining multiple data sources if necessary, filtering, formatting, and loading to target database.

5)	Unit testing
    - Unit test (Data Validation or Data Quality Test) is performed to verify each component in PDI working as expected, to achieve data reliability and accuracy through output verification. May vary in every organization.
    - Operates in staging area using mock or real data.
    - Ensure aspects of: -
        - Data Completeness – Total number input vs output.
        - Data Uniqueness – Is there any duplicate or redundant data.
        - Data Validity – Consistent formatting (schema, data type conversion, whitespaces).
        - Data Consistency – Details input vs output matching.
        - Data Integrity – Check variable relationship after merging data source.
        - Data Compliance & Exclusion – Essential business logic validation (if any) such as additional formulas for calculation, rule filtering (i.e: Quantity and Date range, Null or Invalid, Custom, etc.). 
        - Process errors – Checks overall end-to-end data integration process for any component error that may result in job failure.

6)	Rollout to production environment.
    - Release deployment.
    - Communicate with stakeholders to verify expected outcome.
    - Lead to product’s operation & maintenance phase during warranty period.

## Demonstration of PDI tools in Healthcare OLAP system
1. Example of overall process:
<br/>![Process Overview Image](https://github.com/mokaamil/etl-process/blob/main/process%20overview.png)<br/><br/>
2. Job
    - Runs high level components consist of main processes
<br/>&nbsp;&nbsp;&nbsp;![ETL Job Image](https://github.com/mokaamil/etl-process/blob/main/etl%20job.png)<br/><br/>  
    - The above shows overall process from start, then proceed to ‘visit’ transformation, and end with the main fact. This is simplified view since real data processing scenario require staging area to gather data from source, that are further shown in transformation example.<br/><br/>
3. Transformation
    - A more in-depth look of what each of process does.
    - Let’s take a look a sample of how the ‘inpatient’ data process might be:-
        - Staging
            - The overall process may look like this and more:
<br/>&nbsp;&nbsp;&nbsp;![Staging Sample Image](https://github.com/mokaamil/etl-process/blob/main/staging%20sample.png)<br/><br/>  
            - For general understanding of what PDI does in ‘staging’ step: 
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![ETL Transformation Image](https://github.com/mokaamil/etl-process/blob/main/etl%20transformation.png)<br/><br/>  
            - Starting by addressing the source of data in ‘source_json’. Data source may vary based on the needs of project. In this example, show json as the loading source. Component involved:
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Input Component Image](https://github.com/mokaamil/etl-process/blob/main/input%20component.png)<br/><br/> 
            - The second step is selecting variable in ‘extract_visit’ using the same method. 
            - Then, data is being validate according to the rule in ‘validation’ step. It includes the processing of variable to be sent to error log file. Component involved:
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Validation Component Image](https://github.com/mokaamil/etl-process/blob/main/validation%20component.png)<br/><br/>
            - Further, the data that has passed the validation are being sorted, selected, and lastly saved in ‘tgt_visit_stg’ as the target database storage. Component involved:
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Output Component Image](https://github.com/mokaamil/etl-process/blob/main/output%20component.png)<br/><br/>
        - Visit dimension and Fact
            - Undergo the same process as ‘Staging’. The only differences are the data source will be staging table, validation rule to be made, and target table will be ‘visit_dim’ or ‘inpatient_fact’.
            - Example of real fact process (Incomplete due to confidentiality):
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Fact Sample Image](https://github.com/mokaamil/etl-process/blob/main/fact%20sample.png)<br/><br/>
            - It shows that the real process might have a long list of validation, logic to be implemented, sources and targets, as well as additional process such as update/delete, aggregation, key assignment, and joining tables.

### References

[1] Pentaho Data Integration - <br/>
https://help.hitachivantara.com/Documentation/Pentaho/7.0/0D0/Pentaho_Data_Integration











