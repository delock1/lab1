# Технология разработки программного обеспечения
# Лабораторная работа №2: создание кластера Kubernetes и деплой приложения
## Сметанин Андрей Михайлович, Группа 3МБД2001
## Цель лабораторной работы: 
Целью лабораторной работы является знакомство с кластерной архитектурой на примере Kubernetes, а также деплоем приложения в кластер.

### Манифест deployment.yaml  
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 5
  selector:
    matchLabels:
      app: my-app
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - image: myapi:latest
          # https://medium.com/bb-tutorials-and-thoughts/how-to-use-own-local-doker-images-with-minikube-2c1ed0b0968
          # указыаает на то, что образы нужно брать только из локального registry. В продакшене никогда не использовать
          imagePullPolicy: Never 
          name: myapi
          ports:
            - containerPort: 8080
      hostAliases:
      - ip: "192.168.49.1" # The IP of your VM
        hostnames:
        - postgres.local
 ```
 
 ### Манифест service.yaml
 ```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - nodePort: 31317
      port: 8080
      protocol: TCP
      targetPort: 8080
  selector:
    app: my-app
 
 ```
### Скриншот шага 3.3 
![Снимок3.PNG](Снимок3.PNG "Шаг 3.3")

### Скриншот шага 3.5
![Снимок5.PNG](Снимок5.PNG "Шаг 3.5")
### Видео с обзором созданного кластера  
[Ссылка на видео с обзором](https://yadi.sk/i/rTrQ8T1eT49gJw "Ссылка на видео с обзором")

