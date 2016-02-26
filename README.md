# Demo of Kubernetes on Raspberry PI
### Modules
- simagix/mobile-signature
- simagix/signature-map
- mqtt broker (mosquitto or mqtt://test.mosquitto.org)

### Kubernetes
Start web apps using kubectl
```
kubectl run mobile-signature --image=simagix/mobile-signature-rpi --port=3300 --env="MQTT_BROKER=mqtt://192.168.1.2"
kubectl expose rc mobile-signature --port=3300 --target-port=3300 --external-ip=192.168.1.2
kubectl run signature-map --image=simagix/signature-map-rpi --port=3301 --env="MQTT_BROKER=mqtt://192.168.1.2"
kubectl expose rc signature-map --port=3301 --target-port=3301 --external-ip=192.168.1.2
```

### Get Info
```
kubectl get nodes
kubectl get pods
kubectl get rc
kubectl get svc
```

### Stop Services
```
kubectl delete svc signature-map
kubectl delete rc signature-map
kubectl delete pod signature-map-<some_id>
kubectl delete svc mobile-signature
kubectl delete rc mobile-signature
kubectl delete pod mobile-signature-<some_id>
```

### Docker
Start web apps using docker command.
```
docker run -p 3300:3300 -it -e MQTT_BROKER=mqtt://192.168.1.2 simagix/mobile-signature-rpi
docker run -p 3301:3301 -it -e MQTT_BROKER=mqtt://192.168.1.2 simagix/signature-map-rpi
```