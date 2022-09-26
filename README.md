# migration-s3-to-gcs-using-terraform

## What is S3 bucket?
Amazon Simple Storage Service (Amazon S3) is an object storage service offering industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can store and protect any amount of data for virtually any use case, such as data lakes, cloud-native applications, and mobile apps. With cost-effective storage classes and easy-to-use management features, you can optimize costs, organize data, and configure fine-tuned access controls to meet specific business, organizational, and compliance requirements.

Reffer this doc:- https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingBucket.html

## What is GCS bucket?
Cloud Storage allows world-wide storage and retrieval of any amount of data at any time. You can use Cloud Storage for a range of scenarios including serving website content, storing data for archival and disaster recovery, or distributing large data objects to users via direct download.

Reffer this doc:- https://cloud.google.com/storage/docs

## Why data migration is needed.
Cloud data migration is the procedure of moving information, localhost applications, services, and data to the distributed cloud computing infrastructure. The success of this data migration process is depending on several aspects like planning and impact analysis of existing enterprise systems. One of the most common operations is moving locally stored data in a public cloud computing environment. This paper, through a multivocal literature review, identifies the key advantages and consequences of migrating data into the cloud. There are five different cloud migration strategies and models prescribed to evaluate the performance, identifying security requirements, choosing a cloud provider, calculating the cost, and making any necessary organizational changes. The results of this research paper can give a road map for the data migration journey and can help decision makers towards a safe and productive migration to a cloud computing environment.

Reffer this doc:-https://www.sciencedirect.com/science/article/pii/S1877050919321921

## Migration market revenue 
![image](https://user-images.githubusercontent.com/63963025/189472009-87a5beda-4908-4a33-ad8f-b2318902a334.png)

Reffer this doc:- https://www.mavenwave.com/blog/trends_cloud_migration_financial_services/


## Steps to Migrate S3 to GCS using terraform 
### Step1 create a Virtual machine 
- Go to Navigation menu --> Compute Engine Section --> Create virtual instance 
<img width="1365" alt="image" src="https://user-images.githubusercontent.com/63963025/192267305-e2e80042-f369-473a-9d40-583edce87403.png">
 
- Name your machine and select Region <b>us-central1</b> Zone <b>us-central1-a</b>
<img width="523" alt="image" src="https://user-images.githubusercontent.com/63963025/192268068-0dd36218-f3b8-4468-9104-38b610eb26b8.png">

- Select MAchine Configuration --> Series <b>E2</b> Machine type <b>e2-medium</b> 
<img width="533" alt="image" src="https://user-images.githubusercontent.com/63963025/192268784-f5e28e84-6d4e-4c92-a1a6-b25a330a6eb8.png">

- Boot disk Select image 
