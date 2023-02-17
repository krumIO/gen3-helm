# hatchery

![Version: 0.1.2](https://img.shields.io/badge/Version-0.1.2-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: master](https://img.shields.io/badge/AppVersion-master-informational?style=flat-square)

A Helm chart for gen3 Hatchery

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `100` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| env[0].name | string | `"HTTP_PORT"` |  |
| env[0].value | string | `"8000"` |  |
| env[1].name | string | `"POD_NAMESPACE"` |  |
| env[1].valueFrom.fieldRef.fieldPath | string | `"metadata.namespace"` |  |
| fullnameOverride | string | `""` |  |
| global | map | `{"aws":{"awsAccessKeyId":null,"awsSecretAccessKey":null,"enabled":false},"ddEnabled":false,"dev":true,"dictionaryUrl":"https://s3.amazonaws.com/dictionary-artifacts/datadictionary/develop/schema.json","dispatcherJobNum":10,"environment":"default","hostname":"localhost","kubeBucket":"kube-gen3","logsBucket":"logs-gen3","netPolicy":true,"portalApp":"gitops","postgres":{"dbCreate":true,"master":{"host":null,"password":null,"port":"5432","username":"postgres"}},"publicDataSets":true,"revproxyArn":"arn:aws:acm:us-east-1:123456:certificate","syncFromDbgap":false,"tierAccessLevel":"libre","userYamlS3Path":"s3://cdis-gen3-users/test/user.yaml"}` | Global configuration options. |
| global.aws | map | `{"awsAccessKeyId":null,"awsSecretAccessKey":null,"enabled":false}` | AWS configuration |
| global.aws.awsAccessKeyId | string | `nil` | Credentials for AWS stuff. |
| global.aws.awsSecretAccessKey | string | `nil` | Credentials for AWS stuff. |
| global.aws.enabled | bool | `false` | Set to true if deploying to AWS. Controls ingress annotations. |
| global.ddEnabled | bool | `false` | Whether Datadog is enabled. |
| global.dev | bool | `true` | Whether the deployment is for development purposes. |
| global.dictionaryUrl | string | `"https://s3.amazonaws.com/dictionary-artifacts/datadictionary/develop/schema.json"` | URL of the data dictionary. |
| global.dispatcherJobNum | int | `10` | Number of dispatcher jobs. |
| global.environment | string | `"default"` | Environment name. This should be the same as vpcname if you're doing an AWS deployment. Currently this is being used to share ALB's if you have multiple namespaces. Might be used other places too. |
| global.hostname | string | `"localhost"` | Hostname for the deployment. |
| global.kubeBucket | string | `"kube-gen3"` | S3 bucket name for Kubernetes manifest files. |
| global.logsBucket | string | `"logs-gen3"` | S3 bucket name for log files. |
| global.netPolicy | bool | `true` | Whether network policies are enabled. |
| global.portalApp | string | `"gitops"` | Portal application name. |
| global.postgres | map | `{"dbCreate":true,"master":{"host":null,"password":null,"port":"5432","username":"postgres"}}` | Postgres database configuration. |
| global.postgres.dbCreate | bool | `true` | Whether the database should be created. |
| global.postgres.master | map | `{"host":null,"password":null,"port":"5432","username":"postgres"}` | Master credentials to postgres. This is going to be the default postgres server being used for each service, unless each service specifies their own postgres |
| global.postgres.master.host | string | `nil` | hostname of postgres server |
| global.postgres.master.password | string | `nil` | password for superuser in postgres. This is used to create or restore databases |
| global.postgres.master.port | string | `"5432"` | Port for Postgres. |
| global.postgres.master.username | string | `"postgres"` | username of superuser in postgres. This is used to create or restore databases |
| global.publicDataSets | bool | `true` | Whether public datasets are enabled. |
| global.revproxyArn | string | `"arn:aws:acm:us-east-1:123456:certificate"` | ARN of the reverse proxy certificate. |
| global.syncFromDbgap | bool | `false` | Whether to sync data from dbGaP. |
| global.tierAccessLevel | string | `"libre"` | Access level for tiers. |
| global.userYamlS3Path | string | `"s3://cdis-gen3-users/test/user.yaml"` | Path to the user.yaml file in S3. |
| hatchery.containers[0].args[0] | string | `"--NotebookApp.base_url=/lw-workspace/proxy/"` |  |
| hatchery.containers[0].args[1] | string | `"--NotebookApp.default_url=/lab"` |  |
| hatchery.containers[0].args[2] | string | `"--NotebookApp.password=''"` |  |
| hatchery.containers[0].args[3] | string | `"--NotebookApp.token=''"` |  |
| hatchery.containers[0].args[4] | string | `"--NotebookApp.shutdown_no_activity_timeout=5400"` |  |
| hatchery.containers[0].args[5] | string | `"--NotebookApp.quit_button=False"` |  |
| hatchery.containers[0].command[0] | string | `"start-notebook.sh"` |  |
| hatchery.containers[0].cpu-limit | string | `"1.0"` |  |
| hatchery.containers[0].env.FRAME_ANCESTORS | string | `"https://{{ .Values.global.hostname }}"` |  |
| hatchery.containers[0].fs-gid | int | `100` |  |
| hatchery.containers[0].gen3-volume-location | string | `"/home/jovyan/.gen3"` |  |
| hatchery.containers[0].image | string | `"quay.io/cdis/heal-notebooks:combined_tutorials__latest"` |  |
| hatchery.containers[0].lifecycle-post-start[0] | string | `"/bin/sh"` |  |
| hatchery.containers[0].lifecycle-post-start[1] | string | `"-c"` |  |
| hatchery.containers[0].lifecycle-post-start[2] | string | `"export IAM=`whoami`; rm -rf /home/$IAM/pd/dockerHome; rm -rf /home/$IAM/pd/lost+found; ln -s /data /home/$IAM/pd/; true"` |  |
| hatchery.containers[0].memory-limit | string | `"2Gi"` |  |
| hatchery.containers[0].name | string | `"(Tutorials) Example Analysis Jupyter Lab Notebooks"` |  |
| hatchery.containers[0].path-rewrite | string | `"/lw-workspace/proxy/"` |  |
| hatchery.containers[0].ready-probe | string | `"/lw-workspace/proxy/"` |  |
| hatchery.containers[0].target-port | int | `8888` |  |
| hatchery.containers[0].use-tls | string | `"false"` |  |
| hatchery.containers[0].user-uid | int | `1000` |  |
| hatchery.containers[0].user-volume-location | string | `"/home/jovyan/pd"` |  |
| hatchery.sidecarContainer.args | list | `[]` |  |
| hatchery.sidecarContainer.command[0] | string | `"/bin/bash"` |  |
| hatchery.sidecarContainer.command[1] | string | `"./sidecar.sh"` |  |
| hatchery.sidecarContainer.cpu-limit | string | `"0.1"` |  |
| hatchery.sidecarContainer.env.HOSTNAME | string | `"{{ .Values.global.hostname }}"` |  |
| hatchery.sidecarContainer.env.NAMESPACE | string | `"{{ .Release.Namespace }}"` |  |
| hatchery.sidecarContainer.image | string | `"quay.io/cdis/ecs-ws-sidecar:master"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[0] | string | `"su"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[1] | string | `"-c"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[2] | string | `"echo test"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[3] | string | `"-s"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[4] | string | `"/bin/sh"` |  |
| hatchery.sidecarContainer.lifecycle-pre-stop[5] | string | `"root"` |  |
| hatchery.sidecarContainer.memory-limit | string | `"256Mi"` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"quay.io/cdis/hatchery"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources.limits.cpu | float | `1` |  |
| resources.limits.memory | string | `"512Mi"` |  |
| resources.requests.cpu | float | `0.1` |  |
| resources.requests.memory | string | `"12Mi"` |  |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| tolerations | list | `[]` |  |
| volumeMounts[0].mountPath | string | `"/hatchery.json"` |  |
| volumeMounts[0].name | string | `"hatchery-config"` |  |
| volumeMounts[0].readOnly | bool | `true` |  |
| volumeMounts[0].subPath | string | `"json"` |  |
| volumes[0].configMap.name | string | `"manifest-hatchery"` |  |
| volumes[0].name | string | `"hatchery-config"` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
