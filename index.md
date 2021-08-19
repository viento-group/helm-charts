# Official helm charts repository of Viento group

## Add repository to helm
Run folow commands to add this helm repository:
```bash
$ helm repo add viento-group https://viento-group.github.io/helm-charts
$ helm repo update
```

## Availiable charts
- [kube-monitoring-telegram-bot](#kube-monitoring-telegram-bot-helm-chart)

## kube-monitoring-telegram-bot helm chart
This is official kube-monitoring-telegram-bot helm chart of Viento group.

This chart use [viento-group/kubernetes-monitoring-telegram-bot](https://github.com/viento-group/kubernetes-monitoring-telegram-bot) application for setting up telegram bot, that send notifications, received from Kubewatch and Prometheus Alert Manager.

Example command to run this helm chart:
```bash
$ helm repo add viento-group https://viento-group.github.io/helm-charts
$ helm repo update
$ helm install telegram-bot viento-group/kube-monitoring-telegram-bot --set telegramBot.globalBotToken.use=true --set telegramBot.globalBotToken.token=<telegram-bot-token>
```

### Configuration
#### Image configuration
Key | Default Value | Description
--- | ------------- | -----------
replicaCount | 1 | Count of replicas, that Kubernetes should create.
image.repository | vientoprojects/kubernetes-monitoring-telegram-bot | Image repository.
image.pullPolicy | IfNotPresent | Image pull policy.
image.tag | latest | Tag of image.

#### Global telegram bot configuration
Key | Default Value | Description
--- | ------------- | -----------
telegramBot.globalBotToken.use | false | Should we use telegram global bot.
telegramBot.globalBotToken.existingPasswordSecret | ~ | Password secret name, which collect global telegram bot token. If `~`, `telegramBot.globalBotToken.token` will be used.
telegramBot.globalBotToken.existingPasswordSecretKey | global-bot-token | Password secret key, which collect global telegram bot token.
telegramBot.globalBotToken.token | | Plain telegram global bot token.

#### Kubewatch telegram bot configuration
Key | Default Value | Description
--- | ------------- | -----------
telegramBot.kubewatchBotToken.use | false | Should we use telegram kubewatch bot (if `false`, global bot will be used for sending Kubewatch notifications).
telegramBot.kubewatchBotToken.existingPasswordSecret | ~ | Password secret name, which collect kubewatch telegram bot token. If `~`, `telegramBot.kubewatchBotToken.token` will be used.
telegramBot.kubewatchBotToken.existingPasswordSecretKey | kubewatch-bot-token | Password secret key, which collect kubewatch telegram bot token.
telegramBot.kubewatchBotToken.token | | Plain telegram kubewatch bot token.

#### Prometheus telegram bot configuration
Key | Default Value | Description
--- | ------------- | -----------
telegramBot.prometheusBotToken.use | false | Should we use telegram prometheus bot (if `false`, global bot will be used for sending Prometheus alerts).
telegramBot.prometheusBotToken.existingPasswordSecret | ~ | Password secret name, which collect prometheus telegram bot token. If `~`, `telegramBot.prometheusBotToken.token` will be used.
telegramBot.prometheusBotToken.existingPasswordSecretKey | prometheus-bot-token | Password secret key, which collect prometheus telegram bot token.
telegramBot.prometheusBotToken.token | | Plain telegram prometheus bot token.

#### Application configuration
Key | Default Value | Description
--- | ------------- | -----------
telegramBot.loggingLevel | info | Application logging level. Available: `trace`, `debug`, `info`, `warn`, `error`, `fatal`, `off`.

#### Pod configuration
Key | Description
--- | -----------
pod.labels | Key-value map, that will be applied as a pod labels.
pod.annotations | Key-value map, that will be applied as a pod annotations.
pod.nodeSelector | Key-value map, that will be applied as a pod node selector.

#### Service configuration
Key | Default Value | Description
--- | ------------- | -----------
service.type | ClusterIP | Type of kubernetes service, that will be created.
service.internalPort | 8080 | Internal port, that will be used, for accessing application (application will automaticaly use this port).
service.externalPort | 8080 | External port, on which clients could connect to this service.
