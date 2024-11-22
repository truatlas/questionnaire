# Локальный запуск на UBUNTU 24.10 DeskTop

1. Скачиваем mongodb
2. Устанавливаем mongodb
3. Запускаем mongodb
4. Устанавливаем nodejs 12
5. Скачиваем questionnaire
6. Запускаем dev-режим questionnaire-backend
7. Запускаем dev-режим questionnaire-frontend
8. Проверка работы

---

## 1. Скачиваем mongodb

С сайта https://www.mongodb.com/try/download/community скачиваем _mongodb-org-server_8.0.3_amd64.deb_

## 2. Устанавливаем mongodb

`sudo dpkg -i mongodb-org-server_8.0.3_amd64.deb`

## 3. Запускаем mongodb

```
sudo systemctl enable mongod
sudo systemctl start mongod
```

## 4. Устанавливаем nodejs 12

```
curl -fsSL https://fnm.vercel.app/install | bash
source /home/egor/.bashrc
fnm use --install-if-missing 12
node -v
exit
```

Выходим из терминала.

---

Запускаем **Первый терминал**

---

## 5. Скачиваем questionnaire

`git clone https://github.com/taptima/devops-test-questionnaire.git`

## 6. Запускаем dev-режим questionnaire-backend

```
cd devops-test-questionnaire/questionnaire-backend
npm install
npm run dev
```

---

Запускаем **Второй терминал**

---

## 7. Запускаем dev-режим questionnaire-frontend

```
cd devops-test-questionnaire/questionnaire-frontend
npm install
npm run start
```

---

## 8. Проверка работы

Открываем в браузере http://localhost:4200/

И проверяем работу согласно инструкции https://taptima.notion.site/Devops-9d61f75e266849cc9173ac6c70fc872c

_Проверяем, что приложение запускается и работает корректно._

---

The END.
