# upstream-collector-with-k8s-navigator

This example shows how to use the upstream the OpenTelemetry Collector to monitor a Kubernetes cluster and export the data to Splunk Observability Cloud. 

It uses the [OpenTelemetry Collector Helm Chart](https://opentelemetry.io/docs/kubernetes/helm/collector/) to deploy two types of collectors: 

1) The purpose of the first collector is to collect cluster-level metrics from the Kubernetes API server. It's run using deployment mode, to avoid producing duplicate data. 
2) The purpose of the second collector is to receive, process, and export all other types of data. It's run as using daemonset mode. 

To deploy this example:

1) Edit `configmap.yaml` and `secret.yaml` to input the specific parameters for your environment. 

2) Use the following commands to create the config map and secrets:

`kubectl apply -f ./configmap.yaml`\
`kubectl apply -f ./secret.yaml`

3) Install the Helm repository:

`helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts` \
`helm repo update`

4) Install the two collectors: 

`helm install otel-collector-cluster-receiver open-telemetry/opentelemetry-collector -f ./cluster-receiver-values.yaml` \
`helm install otel-collector-agent open-telemetry/opentelemetry-collector -f ./agent-values.yaml`
