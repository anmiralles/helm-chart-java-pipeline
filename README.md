# README

Pipeline resources:
* The pipeline 
* Some custom Tasks
* The Triggers 
* Supporting resources:
  * PVC
  * Secrets
  * Config Map

```shell
helm install java-pipeline .
```  

Trigger the pipeline
```bash
$ tkn pipeline start java-pipeline \
    -p git-url=https://github.com/anmiralles/quarkus-fruits-api.git \
    -p image=quay.io/rh-ee-amiralle/quarkus-fruits-api \
    -w name=shared-workspace,claimName=java-pipeline-pvc \
    -w name=dockerconfig,secret=quay-secret \
    --use-param-defaults
```

Log progress as shown. If there are two or more running, the shell is interactive to allow you to pick correct log
```shell
$ tkn pipeline logs -f
? Select pipelinerun:  [Use arrows to move, type to filter]
> build-and-deploy-run-xy7rw started 36 seconds ago
  build-and-deploy-run-z2rz8 started 40 seconds ago
```

Re-run last pipeline
```shell
$ tkn pipeline start build-and-deploy --last
```
