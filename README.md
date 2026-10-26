
AWS S3 Static Website Hosting
##################################################################### 
Architecture Diagram




##################################################################### 

Services Used 
Service 		Purpose
Amazon S3		Store static website files
CloudFront	CDN for global content delivery
Route 53		Domain and DNS management
ACM 		  	SSL/TLS certificate management
IAM			    Access control and permissions


##################################################################### 

Permissions Required
Amazon S3 Full Access 
CloudFront Full Access 
Route53 Full Access 
ACM Full Access 


##################################################################### 

Implementation

Create Bucket
Navigate AWS Console → S3 → Create Bucket

Bucket Name: staticsite.bandarkarami.com
Region: ap-south-1 (Mumbai)

Upload files
index.html,

projects/,


Enable Static Website Hosting

Navigate S3 Bucket → Properties

Static Website Hosting : Enable
Index document : index.html

Configure Bucket Policy

Block all public access : Turned Off

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadAccess",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::staticsite.bandarkarami.com/*"
    }
  ]
}

##################################################################### 
 
Create SSL Certificate

Open AWS Certificate Manager(ACM)

Click On Request
 
Click On Request a public certificate and Next
 
Provide domain name
 
Keep the rest setting as default and click Request

Certificate is created.
 
##################################################################### 

Create CloudFront Distribution

Navigate CloudFront and Click on Create Distribution
 
1. Select Plan : Free 

2. Get Started

Enter Distribution name : staticsite.bandarkarami.com
Distribution Type : Single Website or APP
Domain : staticsite.bandarkarami.com

3. Specify Origin 
Origin Type : Amazone S3
S3 Origin : staticsite.bandarkarami.com.s3.*****

4. Enable Security : 
Keep all default setting and click Next
 
5. Get TLS Certificate
Select certificate from ACM created

6. Review and create
Review all setting and click on Create Distribution

##################################################################### 

Configure Route 53

Navigate Route 53 → Hosted Zones

bandarkarami.com

Create Record 
A Name
AAAA Name 
CNAME

##################################################################### 

Test Website

https://staticsite.bandarkarami.com


