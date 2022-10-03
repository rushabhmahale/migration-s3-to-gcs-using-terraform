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

- Boot disk Select image Ubuntu 
<img width="749" alt="image" src="https://user-images.githubusercontent.com/63963025/193495546-74bdff41-297d-420c-b1ca-6fef2da553bd.png">

- Identity and API access Select <b>default compute engine service account </b> and select <b>
Allow full access to all Cloud APIs</b> 
<img width="541" alt="image" src="https://user-images.githubusercontent.com/63963025/193495577-0fc44e6d-2435-4b25-8fba-2ccc8ffc3af9.png">

- Go to Management Console in Availability policies section VM provisioning model select Spot vm 

### What is Spot vm? 
Spot VMs are excess Compute Engine capacity, so their availability varies based on Compute Engine usage. Spot VMs do not have a minimum or maximum runtime.If your workloads are fault-tolerant and can withstand possible VM preemption, Spot VMs can reduce your Compute Engine costs significantly.

Reffer this link:- https://cloud.google.com/compute/docs/instances/spot

- We are using Spot vm here whenever you have usecase for testing scenarios you can select Spot vm this will reduce your costing <b> you can not use this vm for storing your data permently this will delete the vm or stop the vm within 24hrs.</b>

- Standard Price and costing 
<img width="976" alt="image" src="https://user-images.githubusercontent.com/63963025/193496209-4475c661-02ba-45e1-8d3c-a7af0cc024a5.png">


- Spot vm 
<img width="969" alt="image" src="https://user-images.githubusercontent.com/63963025/193496262-5a93e604-1b60-4dc2-8ca8-0e83e1fc05af.png">

- Create your instance 
<img width="1030" alt="image" src="https://user-images.githubusercontent.com/63963025/193496708-1ae1db93-b8a5-43b8-8c26-9ca840ea17de.png">

### Step2 Install terraform inside machine 

- SSH to machine 
<img width="1037" alt="image" src="https://user-images.githubusercontent.com/63963025/193497163-f069115a-9d7d-45e3-afe6-413846b30e02.png">

- Download terraform this link:- https://www.terraform.io/downloads
<img width="667" alt="image" src="https://user-images.githubusercontent.com/63963025/193498184-bfc6764e-131f-4ea0-bcf0-86d501a88cb1.png">

### Step3 terraform Code 
- Provider Google
```
provider "google" {
  project     = "<PROJECT_ID>"
  region      = "<REGION>"
}

```
- GCP Bucketname Project_id 
```
resource "google_storage_bucket" "s3-backup-bucket" {
  name          = "<GCP_BUCKETNAME>"
  storage_class = "NEARLINE"
  project       = "<PROJECT_ID>"
  location      = "US"
}
```

- Create Service account this will attach Storage Admin role to service account 
```
 resource "google_storage_bucket_iam_member" "s3-backup-bucket" {
  bucket     = google_storage_bucket.s3-backup-bucket.name
  role       = "roles/storage.admin"
  member     = <ServiceAccount>
  depends_on = [google_storage_bucket.s3-backup-bucket]
} 
```
- 
