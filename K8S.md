# Запуск на UBUNTU 24.10 DeskTop на minikube docker

Добавляем домен в hosts
`cat questionnaire.local >> /etc/hosts`

# Созадем папку для приложения

`mkdir -p ~/questionnaire`

# Клонируем репозиторий

`git clone https://github.com/taptima/devops-test-questionnaire.git ~/questionnaire

# В каталоге questionnaire-backend/src/environments заменяем environment.prod.ts на environment.ts

`cp questionnaire-backend/src/environment.prod.ts questionnaire-backend/src/environment.ts`

# Забираем вайлы Dockerfile.frontend и Dockerfile.backend

# В каталоге questionnaire-backend/Dockerfile.backend и переименовываем в Dockerfile

`cp questionnaire-backend/Dockerfile.backend questionnaire-backend/Dockerfile`

# В каталоге questionnaire-frontend/Dockerfile.frontend и переименовываем в Dockerfile

`cp questionnaire-frontend/Dockerfile.frontend questionnaire-frontend/Dockerfile`

# Собираем docker-образы и отправляем их в github

```bash
cd ~/questionnaire/questionnaire-backend && docker build -t questionnaire-backend . && docker -t questionnaire-backend /ruatlas/questionnaire:backend-v0.0.1
cd ~/questionnaire/questionnaire-frontend && docker build -t questionnaire-frontend . && docker -t questionnaire-frontend /ruatlas/questionnaire:frontend-v0.0.1
push ruatlas/questionnaire:backend-v0.0.1
push ruatlas/questionnaire:frontend-v0.0.1
```

# Образы готовы и залиты в открытый репозиторий

# Забираем директорию k8s с yaml-файлами

`cp k8s/* ~/questionnaire/`

# Переходим в директорию questionnaire

`cd ~/questionnaire`

# Запускаем minikube

`minikube start`

# Применяем манифесты из папки k8s

`kubectl apply -f k8s`

# Запускаем minikube tunnel

`minikube tunnel`

# Проверяем работу приложения - переходим на http://questionnaire.local/ в браузере

# `minikube service questionnaire-frontend --url`
