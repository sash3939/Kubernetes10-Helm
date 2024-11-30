# Домашнее задание к занятию «Helm»

### Цель задания

В тестовой среде Kubernetes необходимо установить и обновить приложения с помощью Helm.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение, например, MicroK8S.
2. Установленный локальный kubectl.
3. Установленный локальный Helm.
4. Редактор YAML-файлов с подключенным репозиторием GitHub.

<img width="717" alt="Helm" src="https://github.com/user-attachments/assets/af55d578-96aa-4886-a72d-b4dbc1181408">


------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Инструкция](https://helm.sh/docs/intro/install/) по установке Helm. [Helm completion](https://helm.sh/docs/helm/helm_completion/).

------

### Задание 1. Подготовить Helm-чарт для приложения

1. Необходимо упаковать приложение в чарт для деплоя в разные окружения. 
2. Каждый компонент приложения деплоится отдельным deployment’ом или statefulset’ом.
3. В переменных чарта измените образ приложения для изменения версии.

Скачиваем файлы для подготовки деплоя. Файлы, которые применялись в лекции.

```bash
root@kuber:~/Kubernetes10-Helm/helm#  git clone https://github.com/aak74/kubernetes-for-beginners.git
Cloning into 'kubernetes-for-beginners'...
remote: Enumerating objects: 983, done.
remote: Counting objects: 100% (236/236), done.
remote: Compressing objects: 100% (173/173), done.
remote: Total 983 (delta 72), reused 173 (delta 45), pack-reused 747 (from 1)
Receiving objects: 100% (983/983), 2.64 MiB | 1.82 MiB/s, done.
Resolving deltas: 100% (362/362), done.
root@kuber:~/Kubernetes10-Helm/helm# ll
total 12
drwxr-xr-x  3 root root 4096 Nov 29 23:17 ./
drwxr-xr-x  4 root root 4096 Nov 29 23:17 ../
drwxr-xr-x 19 root root 4096 Nov 29 23:17 kubernetes-for-beginners/
root@kuber:~/Kubernetes10-Helm/helm/kubernetes-for-beginners# cp -r 40-helm/ /root/Kubernetes10-Helm/helm/
root@kuber:~/Kubernetes10-Helm/helm/kubernetes-for-beginners# cd ..
root@kuber:~/Kubernetes10-Helm/helm# ll
total 16
drwxr-xr-x  4 root root 4096 Nov 29 23:20 ./
drwxr-xr-x  4 root root 4096 Nov 29 23:17 ../
drwxr-xr-x  5 root root 4096 Nov 29 23:20 40-helm/
drwxr-xr-x 19 root root 4096 Nov 29 23:17 kubernetes-for-beginners/
root@kuber:~/Kubernetes10-Helm/helm# cp -R 40-helm/ /root/Kubernetes10-Helm/helm/
cp: '40-helm/' and '/root/Kubernetes10-Helm/helm/40-helm' are the same file
root@kuber:~/Kubernetes10-Helm/helm# ls -l
total 8
drwxr-xr-x  5 root root 4096 Nov 29 23:20 40-helm
drwxr-xr-x 19 root root 4096 Nov 29 23:17 kubernetes-for-beginners
root@kuber:~/Kubernetes10-Helm/helm# rm -R kubernetes-for-beginners/
root@kuber:~/Kubernetes10-Helm/helm# ls -l
total 4
drwxr-xr-x 5 root root 4096 Nov 29 23:20 40-helm

```

Создаем шаблон на базе данных файлов

<img width="440" alt="template" src="https://github.com/user-attachments/assets/6a58cfac-527d-4055-9353-b2e8236c087d">

Получаем что helm при запуске создаст service(port 80) и deployment(nginx version 1.16.0)

В переменных чарта меняем образ приложения

<img width="404" alt="Change chart" src="https://github.com/user-attachments/assets/85993962-18ad-456e-95ac-e7ba208e1fff">

Смотрим измененный шаблон

<img width="398" alt="Change template" src="https://github.com/user-attachments/assets/4150b52a-6774-4c9c-9b2e-686aefc86261">

------
### Задание 2. Запустить две версии в разных неймспейсах

1. Подготовив чарт, необходимо его проверить. Запуститe несколько копий приложения.
2. Одну версию в namespace=app1, вторую версию в том же неймспейсе, третью версию в namespace=app2.
3. Продемонстрируйте результат.

Проверка

<img width="421" alt="check chart demo" src="https://github.com/user-attachments/assets/8e315f48-a56c-4cbe-aed6-3f908acad76e">

<img width="406" alt="install helm template" src="https://github.com/user-attachments/assets/d3a2c9c9-2466-4b0f-9763-857cb1f56bab">

<img width="499" alt="get all check" src="https://github.com/user-attachments/assets/ab3e8d49-e0a8-4caa-b085-b271fc93d652">

<img width="506" alt="helm list" src="https://github.com/user-attachments/assets/c61344be-4507-4bd9-b187-083194b65379">

Запустим несколько версий приложения

<img width="548" alt="versions apps" src="https://github.com/user-attachments/assets/9d3f8e4f-3a15-468e-8dec-73e41b515db4">

Удалим наш helm demo1 чтобы потом создать новый в namespace из условия задачи

<img width="359" alt="delete helm" src="https://github.com/user-attachments/assets/6c0f3626-769b-4972-963b-c0ccc372ead6">

Создаем helm по заданию в п.2

<img width="666" alt="create helm with 2 apps and namespace" src="https://github.com/user-attachments/assets/46581908-8221-4949-93f0-073e7ff5c6d3">

<img width="397" alt="satus pods in new apps" src="https://github.com/user-attachments/assets/9581c295-2994-422e-900d-9f3f23e04918">

Удаляем helms

<img width="460" alt="delete helm all" src="https://github.com/user-attachments/assets/e9332960-569a-4058-bd94-1c97b2991055">

### Правила приёма работы

1. Домашняя работа оформляется в своём Git репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, `helm`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
