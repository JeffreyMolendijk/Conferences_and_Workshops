# AWS Summit Online notes - Day 1
May 18th, Australia / New Zealand

## Day One Keynote
### History and developments of EC2, including custom hardware. AWS aims to deliver new technologies to meet customer demands, Adam Beavis.
* AWS Nitro removed virtualization overhead. The Nitro chips are the reason that new instance types are released every few months.
* AWS Nitro runs outside of the EC2 server, leaving more performance to the customer. 
* AWS custom silicon chips (e.g. Graviton) designed for scale-out workloads, delivering the highest performance.
* Inferentia for machine learning performance iprovements (for inference). Improved instances for training workflows have also been developed (Trainium). 

### Containers, Peter DeSantis
* 80% of cloud hosted containers run on AWS
* AWS offers 3 separate container options, where other vendors typically offer 1.
* EKS and ECS container surfaces
* AWS Fargate container usage without managing them at the service level, but rather at the task level. Most new users are now using AWS Fargate.
* Containers are popular because they remove the complexity of running your own infrastructure.
* AWS lambda takes this even further, by offering event-based computing, only charging you for the time your event is running. This is often the best tool for the job.
* AWS lambda is now integrated with over 140 AWS services.

### Business analytics, Dorothy Li
* Data generation is expanding exponentially, with user-generated data, log files, IOT etc. you may be collecting more data than you are aware off.
* Experimentation with free books in Amazon Kindle > customers who received free books more frequently became paying customers than those who only received samples. Similar analyses were used in other Amazon offers.
* Data-driver organizations need to develop infrasctructure, democratize their data (security, access to whoever needs it), and put the data to work (analytics).
* Becoming more data driven you need to migrate from legacy on-premise (or self managed) to cloud infrastructure, making the data available to who needs it, and analyzing the data using AI and machine learning.
* Moving from legacy systems to manages services (e.g. Amazong Aurora) removes worries about hardware, capacity, propietary lock-ins / licensing. 
* Aurora has shown improved performance compared to MySQL and PostgreSQL.
* DynamoDB is more suited for non-traditional table data, e.g. spatial data or graph-based databases. AWS offers several ways to migrate databases, including schema conversion tools or access to experts. 
* The database freedom program is suited for migrations from licensed / locked-in legacy solutions.
* Centralizing data in a data lake allows controlled access by employees to the data they require. 
* Building a data lake starts with Amazon S3, to store any type of data. Analytics services can be run on S3 data directly, for example using Athena (SQL queries), EMR for data streaming (e.g. Spark), or analyze log data with Elastic search service, or streaming data with Kinesis.
* Redshift lets you query your data lake with better price performance than other data warehouses.

### Innovating with machine learning, Dorothy Li
* Machine learning in various industries leads to competetive advantages.
* AWS offers different stacks of ML complexity, including a stack for experts. 
* Amazon Sagemaker is the intermediate stack, allowing developed to run ML through an intregrated development environment (Sagemaker Studio) to make the workflows easier and standardized.
* The top layer contains AI services, letting customers use AI without building models from scratch, requiering no previous experience or any coding. (e.g. Amazon personalize / Forecast / Kendra)

### Other new offerings, Peter DeSantis
* Local compute now offered.
* 5G for low latency experiences for sites without network connectivity. AWS Wavelength is the solution for this problem. Currently available in the US, Japan and South Korea. 
* AWS Snow family are hardware built for moving large amounts of data though a device that can be shipped to other locations.

### Commbank, Matt Comyn.
* Digital interactions with over 7 million customers, to provide personalised experiences. 
* Commbank mainly investing around risk, resilience, security. Also around improving / reinventing their applications. Investments in analytics and their customer engine to analyze over 157 billion datapoints.
* AWS instances allowed CommSec to keep up with 4-fold increased trading volumes during COVID times.
* Engineering and expertise from AWS has helped CommBank to use the best practices.


## Selecting AWS services to simplify file storage architecture, Architect
* Data comes in many types (structures vs unstructures).
* With every growing amounts of data, how do we organize and store this data
* We may not want to manage the infrastructure, save costs while getting good performance. Other factors are security, availability and innovation.
* AWS offers a large cloud storage portfolio including storage and backup.
* Build your own solutions require software/hardware, research time, licenses, data protections and ongoing management.
* AWS removes this complexity using manages services.
* AWS elastic storage (EFS) allows automatic data moving from frequently and infrequently accessed data with different storage pricings (cost optimizing). EFS is fully managed, cost optimized, easy to use and highly available.
* Amazon FSx is a windows file server with automatic backups, fully managed, multiple availability zones.

## Everything fails, all the time: Designing for resilience, Rajiv Rajah
* A high tolerance for failure used to be normal, with lengthy fixes and limited rollbacks. 
* Expectations have now been changed where highly reliable systems are expected, with consistent experiences.
* Rapid but smaller changes, by multiple teams are preferred over large changes to systems. 
* Distributed systems can be very complex (many dependencies), a failure in one of the downstream systems can have a negative effect on the experience customer.
* Continuous testing is required.
* "Things fail all the time", but systems should still be resilient.
* Most interruptions are due to operator error, load induces or component/host failure.
* Other interractions are less likely, but have higher impact (e.g. all of internet failure, datacenter fire)
* Multiple options for resilience, including multi-zone, multi-region or multi-zone + multi-region availability systems.
* Impaired availability zone failures will automatically reroute traffic to working nodes.
* Some errors, like operator error could affect the entire system. Therefore, backups stored on S3 are also important to rollback.
* Moving to resilient architecture required automation everywhere, continuous testing of unknows and intergrated observability beyond the infrastructure. 
* Without stress testing you cannot identify the weak spots of the system. AWS now has the AWS Fault Injection Simulator (chaos engineering). This allows you perform controlled testing by injecting errors into the system.
* Very few systems are now static, but more and more are on the cloud and are elastic.
* Try to make changes as small as possible, so you can audit and measure its impact.
* Automating deployment using pipelines lets you audit the process easier than manual processed.
* Redundancy is important in resilience, but not always the answer, especially in fast changing systems.
* Partitioning between your systems increased availability.
* Fractional deployments let you move your changes to a part of your system and only move it further once those systems turn out to be stable.

## Let's ship it: Productionising your proof of concept, James Ousby
* Goals of solutions: Monitor web page availability or increased latency. Assign team members to call rosters. Investigated issues accross logs, metrics and traces.
* Amazon Cloudwatch performs website monitoring to check uptime by regular checks.
* Check website performance using metrics, logs and traces.
* Open Telemetry is an open source solution to generate metrics and traces (no logs yet) suitable for AWS services.
* What you log is important: put as much context in your log statements to enable searching / analyses later.
* AWS X-ray can be used to analyze traces and logs. This lets you easily debug your application.

## Data engineering made easy, Paul Macey
* Working with data used to be very different, where different teams had their own databases/data that were not connected.
* The next step was to add dataservers to combine these data.
* Now the engineering of data has moved to the cloud, letting analysts get more insights and letting data scientists build models.
* However, any platform needs to support many analytical users, with new roles being added all the time. (new use cases)
* A data platform needs to evolve with the new use cases, which is possible with AWS.
* Traditional data stores such as databases and warehouses.
* Glue databew, glue studio, data wrangler, sagemaker data wrangler > AWS data engineering tools.
* AWS glue databrew is perfect for BI developers, business users and analysts/ scientists. It lets you normalize data or transform data without writing code. This tool speeds up your analyses. (About 80% of data work is data preparation)
* Databew can profile your data, clean/normalize, map data lineage (recording any change) and finally automate the whole process.
* A use case could be de-identifying patient S3 data, and saving the anonymous data back to S3 to a new file.
* AWS Glue studio is for those new to Spark, or SQL Devs.
* Glue studio lets you visually create data analysis jobs / workflows.
* Glue studio can infer the schema of your CSV file. The transformation tab can be used to alter your data.
* Part of the workflow includes giving glue the required permission to perform the job, before saving.
* Glue is serverless, doesn't require management.
* AWS data wrangler is a python library, for technical users / data engineer.
* AWS python SDK is much more work than using the new AWS Data Wrangler. Reading an object can be done in a single line. Even connecting to and RDS instance is a singe line. 
* Glue Databrew > Glue Studio > AWS Data wrangler. Least to most complex and increasing functions. 
* Learn AWS data wrangler for Python ETL...

## Datadog live demo, Siti Chen
* Datadog allows the development of data dashboards related to business income and website traffic.
* Datadog has many data integrations including servers (required installing a tool), or AWS.
* One of the demo examples includes a Kubernetes example. The hostmap can let you analyze where the traffic of your container comes from (Azure / AWS / GCP) or the geographical region. This let's you identify areas where container health is affected for troubleshooting.
* Datadog lets you see the dependencies of an app that may be causing problems. You can also view logs.

## Re-thinking analytics architectures in the cloud, Praveen Kumar
* Many businesses are moving from silo'd data to data lakes.
* Best practices for cloud based data lakes: ensure that platform architecture is flexible for future needs / datatypes.  
* Review of data profiling using Glue DataBrew, similar to the talk by Paul Macey.


# AWS Summit Online notes - Day 2
May 19th, Australia / New Zealand

## Day Two Keynote
### Quinton Anderson, Director, Solution Architect
* Second Australian AWS region to be launched in Melbourne.
* Queensland startup CERES tag made an animal tracking service for agriculture. Data in agriculture was lagging behind other industries. Now they can track the location, movements and health of the animals. 
* Autonomous robots by Woodside, to use robots for mobility and data gathering (?). The robots on mining sites are used to map the site (using images and other sensors) > robot localization and mapping. In the long term they want the robot to affect things in the world (perform actions on the site).
* Presagen uses ML to address health issues for women. They use image analysis to address fertility problems. Computer vision can assess the quality of embryos. Female oriented healthcare has historically been underserver. A global network of laboratories provide the medical data that lead to new products (e.g. to solve medical problems). Local laws related to medical data leaving the country was a challenge that AWS helped solve (using regions/edges?).
* Quantum computing for computational capabilities in a rapidly evolving field. Prof. Michelle Simons works in quantum physics to (attempt to?) perform computations in minutes that would otherwise take years. 

## Making the event-driven enterprise a reality using AWS streaming data services, Sam Mokhtari
* Setting up event-driven enterprises, including the requirements and architecture patterns.
* Enterprises go though digital transformations using IoT, enterprise apps, social media or application logs. 
* Analytics maturities differ between enterprises, where maturity leads to shorter time from event measurement  to the time to action. Spreadsheet are slower, big data and machine learning are the next step and finally you can perform analytics as soon as the event happens (event-driven).
* Event-driven analytics requires streaming data technologies (stream ingestion, stream storage, stream analytics, stream integration).
* Leads to automated decision making, insightful dashboards, altering or anomaly detection.
* IoT with data streaming allows for predictive maintenance in industrial sectors, prior to part breakdown.
* Clickstream data is data generated by customer usage of your website/tool. This data lets you group behaviors of the user to update recommendations or push notifications.

## The changing role of the DBA moving to AWS managed database services, Anuja Malik
* Database admin jobs will move from maintenance to a more architect role? AWS takes care of most of the common tasks. Database migration will be an important skill for current DBAs.
* New roles will also include more usage monitoring and optimizing. Database options (parameters) will remain important for DBAs but configurations can be defined on AWS and be pushed to multiple RDS (with configuration auditing).

## Benchmark your cloud maturity: A best practices framework, VMware
* The challenges of the cloud: new cloud management challenges (80% of companies overspend), accidental exposing data (50%), not optimizing cloud workloads (47%). 
* Therefore it is important to set up a cloud center of excellence (CCoE) is a team that establishes guidelines for proper cloud usage, withing the business and between teams. 
* It is important for a CCoE to bring together the different users (groups) of the cloud to take everyones needs into account.
* Most customers can usually save up to 25% on their cloud bills per month, but requires different teams to find these savings. 
* Cloud maturity through financial management, operations and security/compliance.
* Maturation though visibility (report costs, usage, real-time detection), optimization (optimize costs, define standards, prioritize high risk violations/altert service owners), governance/automation (automate cost control, automatically fix, build guardrails), business integration (continuous cost optimizing base on business strategy, manage cloud using KPIs).
* CCoEs take time, so just get started! Identify your cloud stakeholders, how often should these teams meet, is your organization centralized or decentralized?
* Visibility: Classify (tagging) all assets in your business with metadata to allow you to view your infrastructure.
* Once your costs have been tagged you can start monitoring it, but also optimized it. Also let's you more easily identify unused resources (EC2) to shut them down and save money. You can also look to resize instances (e.g. VM that typically uses les than 5% of CPU power).
* Set up automatic alerting to instance owners that are not used much. Set up automatic turn off at expected low usage times (e.g. weekend).
* When changing a workflow, set up alerts if the workflow is expected to exceed the set budget by a set percentage. This lets you take action when needed. Some actions can be taken automatically (delete unused storage, unattached keys).
* Some KPIs: cloud costs per customer, cloud spend as percentage of revenue.

## Lakehouse architecture: Simplifying infrastructure and accelerating innovation, Mary Law
* A data lake lets you store all your data in one place, at a lower cost, allowing it to be queried and analyzed.
* Your data lake needs to be scalable, enables easy data moving, setting up governance and compliance and lets you easily visualize data > (modern lake house architecture).
* Amazon S3 is the best place to build a data lake. Other used tools are AWS glue for data moving.


## Designing for mission critical applications with Amazon Aurora, Igor Izotov
* One size fits all (relational) databases are now likely the best solution except for very basic tasks.
* Applications are now often microservices and different types of data storage are usually required (for different access patterns).
* Types > Relational (Aurora), Key-Value (DynamoDB), Document (Amazon documentDB), In-memory (Amazon Elasticache), Graph (Amazon Neptune), Time-series (Amazon timestream), Ledger (Amazon QLDB), Wide-column (Amazon keyspaces).
* Aurora is MySQL and PostgreSQL compatible, with higher performance (5x-3x) and highly available.
* Aurora detects faults automatically and performs failover automatically, with zero dataloss.
* Failovers won't affect your workflows since the adresses stay the same, making it very resilient.
