# CloudNative PostgresOperator database

## Backup

A backup bucket can be created (with terraform module: `ssh://git@github.com:camaeel/tf-modules//backup-bucket`) and integrated with this helm chart. 
By default helm chart uses External Secrets Operator to provide credentials from Hashicorp Vault. But in case other method of obtaining credentials is the proper one, it can be disabled and a secret containing AWS credentials can be provided by any other means. 

## Restore