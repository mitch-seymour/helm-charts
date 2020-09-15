# helm-charts
Mitch's chart repository

## Install the Chart Repository
Add the chart repository.

```sh
$ helm repo add mitch https://mitch-seymour.github.io/helm-charts

$ helm repo list

# output
NAME 	URL
mitch	https://mitch-seymour.github.io/helm-charts
```

## Use the Chart in a Project
Bootstrap your project
```sh
$ helm create my-kafka-streams-app

$ cd my-kafka-streams-app/

# remove the default templates
$ rm -rf templates/*
```


Pull the chart down.
```sh
$ helm pull mitch/kafka-streams-chart -d charts

# verify
$ ls charts/

# expected output
kafka-streams-chart-0.1.0.tgz
```

Override some values.
```sh
cat <<EOF >values.yaml
kafka-streams-chart:
  topics:
    - name: tweets
      partitions: 4
    - name: users
      partitions: 4
EOF
```

Finally, install the chart.

```sh
$ helm install kafka-streams .

$ kubectl get pods

# example output
NAME                          READY   STATUS      RESTARTS   AGE
grafana-6fdb794598-qx8v7      1/1     Running     0          34s
kafka-7bbfbf8988-cwm6n        1/1     Running     0          34s
kafka-create-topics-lb8h2     0/1     Completed   0          34s
prometheus-6c4fb46c89-drcct   1/1     Running     0          34s
zookeeper-7f76859c8b-l8zw7    1/1     Running     0          34
```

