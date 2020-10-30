# Технология разработки программного обеспечения
# Лабораторная работа №2: создание кластера Kubernetes и деплой приложения
## Сметанин Андрей Михайлович, Группа 3МБД2001
## Цель лабораторной работы: 
Целью лабораторной работы является знакомство с кластерной архитектурой на примере Kubernetes, а также деплоем приложения в кластер.

## Манифест deployment.yaml  
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



Сделать в github/gitlab Markdown-страницу, где указать:
Название дисциплины.
Название лабораторной работы.
ФИО и группу.
Цель лабораторной работы.
Манифесты deployment.yaml и service.yaml в тексте страницы.
Скриншты вывода команды консоли с шага 3.3 на фоне рабочего стола.
Скриншоты графического интерфейса с шага 3.5, где видны поды.
30 секундное видео с обзором созданного кластера и вашимментариями.
