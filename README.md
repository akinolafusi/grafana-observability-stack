# grafana-observability-stack
Grafana Observability Stack

Clone the repo

REQUIREMENTS
Docker Desktop with Kubernetes enabled

Run these commands
Install cert-manager (required by OpenTelemetry Operator)
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.2/cert-manager.yaml

Wait for cert-manager to be ready
kubectl wait --for=condition=ready pod -l app.kubernetes.io/instance=cert-manager -n cert-manager --timeout=120s

Apply observability_setup.yaml file
This installs every tool that is needed for observability of the cluster
Kubectl apply -f observability_setup.yaml

To check the Metrics, Logs and Traces
On left pane under Drill down, you will see them

The traces might not be obvious, you can get the list of the IDs and search on the Trace panel
kubectl port-forward -n observability svc/tempo 3200:3200
Run this on another terminal to get the list of Trace Ids
'''curl -s "http://localhost:3200/api/search?limit=10" | jq -r '.traces[] | .traceID' '''
