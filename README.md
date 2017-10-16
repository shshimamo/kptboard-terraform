# KPTBoard Terraform

```
+--------------------+
| ALB                |
|--------------------|
| TargetGrops        |
| * kptboard         |--+
+--------------------+  |
         |              |
         |              |
         |              |
+--------------------+  |
| EC2                |  |
|--------------------|  |
| Docker             |  |
| * kptboard (Rails) |  |
+--------------------+  |
|    |   |     |   |    |
|    |   |     |   |    |  +---------------------------------------+
|    |   |     |   |    |  | IAM Role                              |
|    |   |     |   |    |  |---------------------------------------|
|    |   |     |   |    |  | kptboard_ecs                          |
|    |   |     |   |    +--| * AmazonEC2ContainerServiceRole       |
|    |   |     |   |       |---------------------------------------|
|    |   |     |   |       | kptboard_ec2                          |
|    |   |     |   +-------| * AmazonEC2ContainerServiceforEC2Role |
|    |   |     |           | * kptboard-ssm                        |
|    |   |     |           +---------------------------------------+
|    |   |     |
|    |   |   +----------------------+
|    |   |   | ECR                  |
|    |   |   |----------------------|
|    |   |   | Repository           |
|    |   |   | * kptboard           |
|    |   |   +----------------------+
|    |   |
|    |  +----------------------+
|    |  | ECS                  |
|    |  |----------------------|
|    |  | Service              |
|    |  | * kptboard           |
|    |  | Task                 |
|    |  | * kptboard           |
|    |  | * kptboard-migration |
|    |  +----------------------+
|    |
|  +--------------------------+
|  | SSM Parameter Store      |
|  |--------------------------|
|  | kptboard.database.url    |
|  | kptboard.secret.key.base |
|  +--------------------------+
|
|  +--------------------+
+--| RDS                |
   |--------------------|
   | MySQL              |
   | * kptboard         |
   +--------------------+
```
