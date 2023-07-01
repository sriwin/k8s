# Kubernetes - Commands

# Encrypt & Decrypt Files using Open SSL Password
- use the below commands to encrypt or decrypt files using the password

## Encryption Command
- Note : xyz is the password

```shell
openssl enc -aes-256-cbc -salt -in dec-file.dat -out enc-file.enc -md md5 -k "xyz" -md md5
```

## Decryption Command
- Note : xyz is the password

```shell
openssl enc -d -aes-256-cbc -in enc-file.enc -out dec-file.dec -k "xyz" -md md5
```

# Encryption & Decryption using Private and Pubic Keys
- use the below commands to encrypt or decrypt files using the password

| # | Info | Additional Notes
|:--:|:-----|
|1|Generate Keys|Refer below for details




## Kubernetes - kubectl Commands

### All Commands 

| Command                                                                                            |Notes|
|:---------------------------------------------------------------------------------------------------|:--- |
| kubectl get pods                                                                                   |
| kubectl get pods -o wide                                                                           |
| kubectl get services                                                                               |
| kubectl get configmap                                                                              |
| kubectl get secrets                                                                                |
| kubectl get ingress                                                                                |
| kubectl get pods -l=app=<name>                                                                     |
| kubectl get deployments                                                                            |
| kubectl get service <name>                                                                         |
| kubectl get secrets --field-selector metadata.name=<name>                                          |
| kubectl describe pods                                                                              |
| kubectl describe ingress                                                                           |
| kubectl describe services                                                                          |
| kubectl describe configmap                                                                         |
| kubectl describe deployments                                                                       |
| kubectl edit pod <name>                                                                            |
| kubectl edit configmap <name>                                                                      |
| kubectl edit service <name>                                                                        |
| kubectl edit ingress <name>                                                                        |
| kubectl logs -f <pod-name>                                                                         |
| kubectl delete -f <app-yml-file>                                                                   |
| kubectl delete deployment <name>                                                                   |
| kubectl delete deployment <name>                                                                   |
| kubectl delete service <name>                                                                      |
| kubectl delete secret <name>                                                                       |
| kubectl delete pods,deploy,svc,cm,ingress --all --grace-period=0 --force --namespace <namespace>   |
| kubectl apply <app-yml-file>                                                                       |
| kubectl create cm <cm-name> --from-file=<configmap.yam>l -n <ns>                                   |
| kubectl get events                                                                                 |
| kubectl config get-contexts                                                                        |
| kubectl config current-context                                                                     |
| kubectl config use-context                                                                         |
| kubectl config set-context <host> --namespace=<namespace>                                          |
| kubectl scale deployment <name> --replicas=0 -n <ns>                                               |
| kubectl scale deployment <name> --replicas=0 -n <ns>                                               |
| kubectl create namespace "$K8S_NS"                                                                 || true                            |
| kubectl config set-credentials "${K8S_USER}" --token="${K8S_PASS}"                                 || true                            |
| kubectl config set-cluster "${K8S_CLUSTER}" --server="${K8S_SERVER_URL}"                           |
| kubectl config set-cluster "${K8S_CLUSTER}" --insecure-skip-tls-verify=true                        |
| kubectl config set-context "${K8S_CONFIG_CONTEXT}" --cluster="${K8S_CLUSTER}" --user="${K8S_USER}" |
| kubectl config use-context "${K8S_CONFIG_CONTEXT}"                                                 |
| kubectl config set-context "${K8S_CONFIG_CONTEXT}" --cluster="${K8S_CLUSTER}" --user="${K8S_USER}" |

-  Delete all pods
```shell
kubectl get pods --no-headers=true -l=<app-name> | awk '{print $1}' | xargs kubectl delete pod
```

### kubectl create secrets

```shell
kubectl create secret generic <app-name> --from-file secrets.yml  --namespace = <ns> -o yaml --dry-run=client --save-config | kubectl apply -f 

kubectl delete secret <secretName>
kubectl create secret docker-registry "${secretName}" -n "${namespace}" --docker-username="${username}" --docker-password="${password}" --docker-email=<email> --docker-server="$dockerServer" --dry-run=client --save-config -o yaml | kubectl apply -f -

kubectl get pods --field-selector=status.phase=Running -n "$K8S_NS" -l release="$HELM_APP_NAME" | grep Running > "${HELM_APP_NAME}"_helmsafetynet.tmp || true

kubectl get deploy -l release="$HELM_APP_NAME" -n "$K8S_NS" -o yaml > "${HELM_APP_NAME}"_"${CURRENT_TIME}"_helmsafety.yaml || true
```


### Logging into Pod & executing commands

```shell
1. Execute the below command
		kubectl exec -it <POD-NAME> -- /bin/sh
2. Enter any of the below command
wget -S https://host:port
curl -v https://host:port
echo $PATH
```

## Helm Commands

| Command                                                  | Notes                                                      |
|:---------------------------------------------------------|:-----------------------------------------------------------|
| helm version --client                                    |                                                            |
| helm list                                                |                                                            |
| helm env                                                 | Helm client environment                                                           |
| helm install [app-name] [chart]                          | Install an app:                                            |
| helm install [app-name] [chart] --namespace [namespace]  | Install an app in a specific namespace                     |
| helm install [app-name] [chart] --values [yaml-file/url] | Override values                                            |
| helm install [app-name] --dry-run --debug                | Run test to validate and verify the chart                  |
| helm uninstall [release]                                 | Uninstall a release                                        |
| helm uninstall [release]                                 | Uninstall a release                                        |

- Other Commands

```shell
helm delete "${HELM_PURGE_PARAM}" "${HELM_KEEP_HISTORY_PARAM}" "${HELM_APP_NAME}" 
"helm uninstall ${HELM_APP_NAME} ${HELM_KEEP_HISTORY} -n ${K8S_NS} ${HELM_DRY_PARAM} ${HELM_DEBUG} || true" 

helm upgrade --install "${HELM_APP_NAME}" "${HELM_CHART_DIR}" -f "${HELM_VALUES}" --namespace="${K8S_NS}" --tiller-namespace="${TILLER_NAMESPACE}" --timeout "${HELM_TIMEOUT}" ${HELM_ADDITIONAL_PARAM} ${HELM_DRY_PARAM} ${HELM_WAIT_PARAM} ${HELM_DEBUG_PARAM} ${HELM_FORCE_PARAM}

helm plugin install https://github.com/databus23/helm-diff
helm diff upgrade "${HELM_APP_NAME}" "${HELM_CHART_DIR}" --values "${HELM_VALUES}" --namespace="${K8S_NS}"
helm upgrade --install "${HELM_APP_NAME}" "${HELM_CHART_DIR}" -f "${HELM_VALUES}" --namespace="${K8S_NS}" --timeout "${HELM_TIMEOUT}" --history-max "${HELM_HISTORY_MAX}" ${HELM_ADDITIONAL_PARAM} ${HELM_DRY_PARAM} ${HELM_WAIT_PARAM} ${HELM_DEBUG_PARAM} ${HELM_FORCE_PARAM}

helm registry login --password "$PASSWORD" -u "$USER" "$REGISTRY"
helm chart pull "$HELM_REPO"
helm chart export --destination "$EXTRACT_DIR" "$HELM_REPO"

```



## Pivotal Cloud Foundry - PCF Commands



| Description                     | Command                                                                  | Notes
|:--------------------------------|:-------------------------------------------------------------------------|:--------|
| Login into PCF                  | cf login --skip-ssl-validation -a <URL> -u <USER-ID> -o <ORG> -s <SPACE> |
| Verify Spaces                   | cf spaces                                                                |
| switch to a different space     | cf target -s <SPACE>                                                     |
| Restart App                     | cf restart <APP-NAME>                                                    |
| Restage App                     | cf restage <APP-NAME>                                                    |
| Tail logs of app                | cf logs <app-name>                                                       |
| Recent logs of app              | cf logs <app-name> --recent                                              |
| List Services                   | cf services                                                              |
| Create Service                  | cf cups <db-service-name> -p "jdbcUrl, username, password"               |enter jdbcUrl, username, password when prompted
| bind service with app           | cf bind-service <app-name> <svc-name>                                    |
| unbind service with app         | cf unbind-service <app-name> <svc-name>                                  |
| delete service                  | cf delete-service <svc-name> -f                                          |
| Rename Service                  | cf rename-service <OLD-NAME> <NEW-NAME>                                          |
| Get Details of Service Instance | cf service <SERVICE-NAME>|
| Create Service using JOSN       | | Refer below for details

- Create Service using JSON

```shell
01. cf login
02. cf services
03. cf unbind-service <app-name> <svc-name>
05. cf delete-service <svc-name> 
06. update json file (label & searchPaths)
07. cf create-service p-config-server standard <svc-name> -c <json-file-with-ext>
08. cf services 
    -> should change "create in progress" to "create succeeded"
09. cf bind-service <app-name> <svc-name>
10. cf restage <app-name>
```
