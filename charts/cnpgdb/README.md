# CloudNative PostgresOperator database

## Backup

A backup bucket can be created (with terraform module: `ssh://git@github.com:camaeel/tf-modules//backup-bucket`) and integrated with this helm chart. 
By default helm chart uses External Secrets Operator to provide credentials from Hashicorp Vault. But in case other method of obtaining credentials is the proper one, it can be disabled and a secret containing AWS credentials can be provided by any other means. 

## Restore

### Logical backup

1. Download backup
2. Decrypt with age: `age -d -i key.txt -o - SRC_BACKUP.sql.gz.age  | gunzip --to-stdout - > backup.sql`
3. Port-forward: `kubectl port-forward svc/example-app-cnpgdb-rw 5432`
4. Restore:
    ```shell
    PGPASSWORD=`kubectl get secret example-app-cnpgdb-app -ojson | jq -r '.data.password' | base64 -d` psql -d DATABASE -U USER -h 127.0.0.1 < backup.sql`
    ```