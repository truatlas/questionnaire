# Запуск на UBUNTU 24.10 DeskTop на minikube docker

## У вас уже установлены wget, minikube(enabled ingress), docker в системе

## Добавляем домен questionnaire.local в hostsmini

`echo 127.0.0.1 questionnaire.local | sudo tee -a /etc/hosts`

## Создаем папку для приложения

`mkdir -p ~/questionnaire`

## Клонируем репозиторий с заданием

`git clone https://github.com/taptima/devops-test-questionnaire.git ~/questionnaire`

## В каталоге questionnaire-backend/src/environments заменяем environment.prod.ts на environment.ts

`cp ~/questionnaire/questionnaire-backend/src/environments/environment.prod.ts ~/questionnaire/questionnaire-backend/src/environments/environment.ts`

## Забираем файлы Dockerfile.frontend и Dockerfile.backend из этого репозитория

```bash
cd ~/questionnaire
wget https://raw.githubusercontent.com/truatlas/questionnaire/refs/heads/main/Dockerfile.backend
wget https://raw.githubusercontent.com/truatlas/questionnaire/refs/heads/main/Dockerfile.frontend
```

## Копируем файл для сборки Dockerfile.backend в каталог questionnaire-backend/Dockerfile.backend и переименовываем в Dockerfile

`cp ~/questionnaire/Dockerfile.backend ~/questionnaire/questionnaire-backend/Dockerfile`

## Копируем файл для сборки Dockerfile.frontend в каталог questionnaire-frontend/Dockerfile.frontend и переименовываем в Dockerfile

`cp ~/questionnaire/Dockerfile.frontend ~/questionnaire/questionnaire-frontend/Dockerfile`

## Собираем docker-образы и отправляем их в github

```bash
cd ~/questionnaire/questionnaire-backend
docker build -t questionnaire-backend:v0.0.1 .
docker image tag questionnaire-backend:v0.0.1 ruatlas/questionnaire:backend-v0.0.1
cd ~/questionnaire/questionnaire-frontend
docker build -t questionnaire-frontend:v0.0.1 .
docker image tag questionnaire-frontend:v0.0.1 ruatlas/questionnaire:frontend-v0.0.1
docker push ruatlas/questionnaire:backend-v0.0.1
docker push ruatlas/questionnaire:frontend-v0.0.1
```

## Образы готовы и залиты в открытый репозиторий

[https://hub.docker.com/repository/docker/ruatlas/questionnaire/general]

## Забираем директорию k8s из этого репозитория и копируем ее в директорию questionnaire

`cp k8s/ ~/questionnaire/`

## Переходим в директорию questionnaire

`cd ~/questionnaire`

## Запускаем minikube

```bashc
minikube start
minikube addons enable ingress
```

## Применяем манифесты из папки k8s, ждем пока все поды будут готовы и запускаем tunnel

```bash
kubectl apply -f k8s

kubectl get pods -n questionnaire -w

minikube tunnel
```

## Проверяем работу приложения - переходим на [http://questionnaire.local/] в браузере

### `minikube service questionnaire-frontend --url`
