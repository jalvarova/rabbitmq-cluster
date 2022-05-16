<h1 id="rabbitmq">Cluster Rabbitmq</h1>

### Install Rabbitmq Operators

```bash
$ kubectl apply -f https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml
```

### Install PriorityClass

```bash
$ kubectl apply -f ./rabbitmq/high-priority.yaml -n rabbitmq-system
```

### Install Cluster Operator Rabbitmq

```bash
$ kubectl apply -f ./rabbitmq/rabbitmq-cluster.yml -n rabbitmq-system
```

### Delete Cluster Operator Rabbitmq

```bash
$ kubectl delete -f  ./rabbitmq/rabbitmq-cluster.yml -n rabbitmq-system
```

### Port Forward al service de rabbitmq

```bash
$ kubectl port-forward svc/rabbitmq-ready 45672:15672 4672:5672 -n rabbitmq-system
```

### Obetner user y password por default

```bash
$ kubectl get secret rabbitmq-ready-default-user -o jsonpath='{.data.username}' -o go-template="{{.data.username | base64decode}}" -n rabbitmq-system
$ kubectl get secret rabbitmq-ready-default-user -o jsonpath='{.data.password}' -o go-template="{{.data.password | base64decode}}" -n rabbitmq-system
```

### Delete Cluster Rabbitmq

```bash
$ kubectl delete -f ./rabbitmq/rabbitmq-cluster.yml -n rabbitmq-system
```

### Rabbitmq Cluster 

![backend](./img/rabbitmq-cluster.png)

### Create User Rabbitmq

![backend](./img/rabbitmq-user.png)

### Import Broker Definitions

![backend](./img/rabbitmq-upload.png)

### Queue 

![backend](./img/rabbitmq-queue.png)

### Post message queue

```json
{
    "productCode": "900",
    "skuCode": "171155",
    "productType": "ST",
    "description": "CAMPANA",
    "price": 509.0,
    "weight": 1.0,
    "width": 1.0,
    "length": 1.0,
    "height": 1.0,
    "unitMeasurement": "UN",
    "hierarchyCode": "L0123"
}
```
![backend](./img/rabbitmq-publish-message.png)

### References

[Rabbit Cluster Operation](https://github.com/rabbitmq/cluster-operator)

[Rabbit Create Cluster](https://github.com/rabbitmq/cluster-operator/tree/main/docs/examples/production-ready)

[Definition Cluster Operation](https://www.rabbitmq.com/kubernetes/operator/using-operator.html)