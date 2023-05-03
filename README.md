# AWS S3 Bucket Policy and CORS Configuration for Specific Domains

This repository contains examples of an Amazon S3 bucket policy and CORS configuration that restrict access to specific domains. The bucket policy allows `GET` and `PUT` operations from the specified domains, while the CORS configuration enables cross-origin resource sharing for the same domains.

## Prerequisites

- An AWS account with access to Amazon S3.
- An existing Amazon S3 bucket that you want to configure.

## Usage

### 1. Configure CORS

Navigate to your S3 bucket in the [AWS Management Console](https://console.aws.amazon.com/s3/), click on the "Permissions" tab, and then click on the "Cross-origin resource sharing (CORS)" button.

Copy the CORS configuration from `cors.json` in this repository and replace the `AllowedOrigins` values with your specific domain names:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": [
                  "https://domain1.com/*",
                   "http://domain2.com/*"
    ],
    "ExposeHeaders": []
  }
]

````
Paste the updated JSON into the CORS configuration editor and click "Save changes.

### 2. Configure Bucket Policy

Navigate to your S3 bucket in the [AWS Management Console](https://console.aws.amazon.com/s3/), click on the "Permissions" tab, and then click on the "Bucket policy" button.

Copy the bucket policy from `bucket-policy.json` in this repository and replace the Resource value with your bucket's ARN, and replace the `aws:Referer` values with your specific domain names:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowGetAndPutFromSpecificDomains",
      "Effect": "Allow",
      "Principal": "*",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::<your-bucket-name>/*",
      "Condition": {
        "StringLike": {
          "aws:Referer": [
            "https://domain1.com/*",
            "http://domain2.com/*"
            
          ]
        }
      }
    }
  ]
}


````
Paste the updated JSON into the bucket policy editor and click "Save changes."
