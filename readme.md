# Weather Forecast demo with Dapr

Forecast API is exposed withing this demo.
Dapr sidecar is attached and Cron input binding triggers calls to the endpoint periodically. 

Config: Open

Tracing: Zipkin, OpenTelemetry (to be added)

Stats & metrics: Prometheus, Grafana

---

Namespace: weather-forecast

App: weather

Service: forecast

Container: forecast-api

---

## How to run

1. Debug (Dapr starts automatically)

`dotnet run`

2. Docker Compose (sets TAG to 1.0)

`docker compose --env-file ./values.env up -d`

3. Kubernetes (Minikube)

a. Set up Minikube cluster as described on https://github.io/robertvejvoda/minikube

b. Deploy code from helm folder (kubectl/helm)

`helm install -f values.yaml weather .`

See logs: `kubectl logs -l service=zipkin -c zipkin --namespace weather-forecast -f`

c. Clean up when finished

`helm uninstall -f values.yaml weather .`

## How to test

Depends on how it's run, navigate to zipkin address http://localhost:9411/zipkin. There should be records from scheduler run. If page is not reachable, make sure to port-forward service `k port-forward svc/zipkin 9411:9411 -n weather-forecast`



