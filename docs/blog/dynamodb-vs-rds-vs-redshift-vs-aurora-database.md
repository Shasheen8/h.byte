---
title: The difference between DynamoDb, RDS, Redshift and Aurora Database
date: Wed, 07 Dec 2022 17:21:00 +0000
---

## DynamoDB

**Amazon DynamoDB** is a fully managed, serverless, key-value NoSQL database designed to run high-performance applications at any scale. DynamoDB offers built-in security, continuous backups, automated multi-Region replication, in-memory caching, and data import and export tools.

-   It provides optional encryption at rest integrated with KMS.
-   The primary resource is a table. No resource-based policies. Full access to a table requires access to not only the `table/<name>` resource but also `table/<name>/*`
-   For fine-grained access, several condition keys are used, including `dynamodb:LeadingKeys`, `dynamodb:Select`, `dynamodb:Attributes`
-   A few pre-existing policies: `AmazonDynamoDBReadOnlyAccess`, `AmazonDynamoDBFullAccess`
-   It provides fine-grained permission: `LeadingKeys` and a substitution variable are used to access items where the partition key matches the self (web identity) user ID by using.
-   API calls like Get and Put are not logged within CloudTrail
-   One can make use of an existing VPC endpoint.
-   It integrates with Cognito an identity pool with roles configured. These roles have a suitable policy to allow Cognito to consider them and to achieve desired DynamoDB actions.

## Relational Database Service (RDS)

**Amazon Relational Database Service (Amazon RDS)** is a collection of managed services that makes it simple to set up, operate, and scale databases in the cloud.

-   IAM controls database instances within RDS. Each instance type has its distinct permission model for handling the database, and a master user is created with the instance.
-   Different resources exist, with the primary being an instance- DB in the arn. There are no resource-based policies.
-   'RDS Encryption' performs encryption at rest, set during creation, and uses KMS. It covers databases, backups, different snapshots, and replicas.
-   It provides transparent data encryption for SQL Server and Oracle using CloudHSM.
-   There's a single root of trust \[tls cert] for all RDS databases where each engine uses its method for connecting over TLS.
-   Manifests are network interfaces within subnets with security groups attached to the interfaces. One can specify a "dB subnet group" - a cluster of subnets it can use to put interfaces in.
-   The "Publicly accessible" option controls whether there is a publicly resolvable DNS name for the instance. It still needs appropriate security group rules.

## Redshift

**Amazon Redshift** uses SQL to analyze structured and semi-structured data across data warehouses, operational databases, and data lakes using AWS-designed hardware and machine learning to deliver the best price-performance at any scale.

-   It provides cluster management with IAM and database user accounts for DB permissions (SQL).
-   With custom Amazon Redshift JDBC \[java database connectivity] or ODBC \[open database connectivity] drivers, one can authenticate via IAM and get quick DB user creds. It provides access to existing users or creates new users.
-   Lots of resources exist with one primary cluster. No resource-based policies. Managed policies are used to give access to all resources, such as `AmazonRedshiftFullAccess` and `AmazonRedshiftReadOnlyAccess`.
-   Clusters are associated with 1+ security groups. It does not appear as an interface in a subnet. Contrast with RDS and DynamoDB - all different combos of network access control.
-   Audit logs are disabled by default (as well as the standard CloudTrail logs). Bucket policy has to allow `putobject` and `getacl` to a specific user from a redshift AWS account that varies by region: `arn:aws:iam::<redshift regional account id>:user/logs`.
-   A big symmetric encryption key hierarchy is present. Optional encryption at rest. With KMS or CloudHSM Classic (only).

## Aurora

**Amazon Aurora** provides built-in security, continuous backups, serverless computing, 15 read replicas, automated multi-Region replication, and integrations with other AWS services.

-   It provides similar capabilities as other RDS engines, except for supporting IAM database authentication.
-   Ability to attach identity policies to IAM principals that allow `rds-dB:connect` for a resource that is a particular database user you create in a specific way in the DB. You get a 'token' from the RDS API by specifying the dB and user, then use the token in place of the user's password when connecting usually. You manage user permissions within the DB as usual - IAM is used for authentication.
-   Uses regular VPC security groups to control access within a VPC.
-   It has its own 'DB security group' to prevent access from outside the VPC - security groups in other VPCs/accounts or the internet. The other RDS engines only use DB security groups in EC2 classic when a VPC isn't available.

## References

-   [https://aws.amazon.com/dynamodb/](https://aws.amazon.com/dynamodb/)
-   [https://aws.amazon.com/rds/](https://aws.amazon.com/rds/)
-   [https://aws.amazon.com/redshift/](https://aws.amazon.com/redshift/)
-   [https://aws.amazon.com/rds/aurora/](https://aws.amazon.com/rds/aurora/)