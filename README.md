| PROMPT | EXAMPLE |
|---|---|
| Створіть маніфест Pod з назвою "app", мітками "app: demo, run: demo", одним контейнером з зображенням "gcr.io/k8s-k3s/demo:v1.0.0" та портом "8000" з назвою "http". | ![](/yaml/app.yaml) |
| Створіть маніфест Pod з назвою "app-volume". Використовуйте контейнер з зображенням "gcr.io/kuar-demo/kuard-amd64:1" і назвою "app". Додайте пробу наявності, яка виконує HTTP запит на шлях "/healthy" і порт 8080 з початковим затриманням 5 секунд, тайм-аутом 1 секундою, періодом 10 секунд і порогом невдач 3. Також додайте пробу готовності, яка виконує HTTP запит на шлях "/ready" і порт 8080 з періодом 2 секунди, початковим затриманням 0 секунд і порогами невдачі 3 та успіху 1. Встановіть порт контейнера 8080 з назвою "http". Для монтування тома використайте шлях "/data" з назвою тома "data". Крім того, додайте том з назвою "data", який використовує тип hostPath і має шлях "/var/lib/app" на хост-системі. | ![](/yaml/app-volumeMounts.yaml) |
| Створіть маніфест Pod з назвою "app-secret". Використовуйте контейнер з назвою "mypod" та зображенням "redis". Для контейнера налаштуйте монтування тома з назвою "foo" і шляхом монтування "/etc/foo". Встановіть опцію "readOnly" на значення "true". Додайте том з назвою "foo", який використовує тип "secret" і має назву секрету "simple-secret". | ![](/yaml/app-secret.yaml) |
| Створіть маніфест Pod з назвою "app-secret-env". Використовуйте контейнер з назвою "mycontainer" та зображенням "redis". Встановіть змінні середовища "SECRET_USERNAME" і "SECRET_PASSWORD" зі значеннями, які витягуються з секрету "mysecret1" з ключами "username" і "password" відповідно. Встановіть політику перезапуску "Never". | ![](/yaml/app-secret-env.yaml) |
| Створіть маніфест Pod з назвою 'app-resource'. Використайте контейнер з зображенням 'gcr.io/kuar-demo/kuard-amd64:1' і назвою 'app'. Додайте проби наявності і готовності. Для проби наявності виконайте HTTP запит на шлях '/healthy' і порт 8080 з початковим затриманням 5 секунд, тайм-аутом 1 секундою, періодом 10 секунд і порогом невдач 3. Для проби готовності виконайте HTTP запит на шлях '/ready' і порт 8080 з періодом 2 секунди, початковим затриманням 0 секунд і порогами невдачі 3 та успіху 1. Встановіть порт контейнера 8080 з назвою 'http'. Для ресурсів встановіть обмеження та запити для CPU і пам'яті: '100m' для CPU і '128Mi' для пам'яті для обох, та обмеження '256Mi' для пам'яті. | ![](/yaml/app-resources.yaml) |
| Створіть маніфест Pod з назвою 'app-readinessprob'. Використовуйте контейнер з зображенням 'gcr.io/k8s-k3s/demo:v2.0.0' і назвою 'app'. Додайте проби наявності та готовності. Для проби наявності виконайте HTTP запит на шлях '/' і порт 8000 з початковим затриманням 5 секунд, тайм-аутом 1 секундою, періодом 10 секунд і порогом невдач 3. Для проби готовності виконайте HTTP запит на шлях '/ready' і порт 8000 з періодом 2 секунди, початковим затриманням 0 секунд і порогами невдачі 3 та успіху 1. Встановіть порт контейнера 8000 з назвою 'http'. | ![](/yaml/app-readinessProbe.yaml) |
| Створіть маніфест Pod з назвою "app-multi-containers". Визначте том з назвою "html", який використовує тип "emptyDir". Додайте контейнер з назвою "1st" і зображенням "nginx". Налаштуйте монтування тома "html" на шлях "/usr/share/nginx/html" для цього контейнера. Додайте ще один контейнер з назвою "2nd" і зображенням "debian". Також налаштуйте монтування тома "html" на шлях "/html" для цього контейнера. Встановіть команду контейнера "2nd" на ["bin/sh", "-c"] і аргументи команди, що записують поточну дату в файл "/html/index.html" кожну секунду за допомогою циклу while true. | ![](/yaml/app-multicontainer.yaml) |
| Створіть маніфест Pod з назвою 'app-livenessprob' у просторі імен 'demo'. Використовуйте контейнер з зображенням 'gcr.io/k8s-k3s/demo:v1.0.0' і назвою 'app'. Додайте пробу наявності, що виконує HTTP запит на шлях '/' і порт 8000 з початковим затриманням 5 секунд, тайм-аутом 1 секундою, періодом 10 секунд і порогом невдач 3. Встановіть порт контейнера 8080 з назвою 'http'. | ![](/yaml/app-livenessProbe.yaml) |
| Створіть маніфест Job з назвою 'app-job-rsync'. Використайте версію API 'batch/v1' та тип 'Job'. У відповідному блоку 'metadata' встановіть назву 'app-job-rsync'. У блоку 'spec' використайте 'template' для визначення контейнерів та об'єктів шаблону. Створіть том з назвою 'data-input', який використовує постійний диск GCE з іменем 'glow-data-disk-200' та типом файлової системи 'ext4'. Додайте контейнер з назвою 'init' та зображенням 'google/cloud-sdk:275.0.0-alpine'. Задайте команду контейнера для виконання rsync між хмарним сховищем і каталогом '/data/input'. Монтуйте том 'data-input' на шлях '/data/input' в контейнері. Встановіть політику перезапуску на 'Never' та обмеження затримки (backoffLimit) на 0. | ![](/yaml/app-job.yaml) |
| Створіть маніфест CronJob з назвою 'app-cronjob'. Використайте версію API 'batch/v1beta1' та тип 'CronJob'. У відповідному блоку 'metadata' встановіть назву 'app-cronjob'. У блоку 'spec' визначте розклад задач за допомогою рядка '*/5 * * * *'. Використайте 'jobTemplate' для визначення шаблону задачі. У шаблоні використовуйте контейнер з назвою 'hello' та зображенням 'bash'. Задайте команду контейнера для виведення рядка 'Hello world'. Встановіть політику перезапуску на 'OnFailure'. | ![](/yaml/app-cronjob.yaml) |
| Створіть маніфест Pod з назвою 'app-config'. Використовуйте версію API 'v1' та тип 'Pod'. У блоку 'metadata' встановіть назву 'app-config'. У блоку 'spec' визначте контейнер з назвою 'mypod' та зображенням 'redis'. Встановіть політику отримання зображення як 'Always'. Визначте змінну середовища з назвою 'CONFIGMAP_PARAM', яка отримує значення з об'єкту configMapKeyRef з назвою 'app-config' та ключем 'config-param'. Додайте точку монтування тому з назвою 'config-volume' на шлях '/config' у контейнері. Визначте том з назвою 'config-volume', який використовує об'єкт configMap з назвою 'app-config'. Встановіть політику перезапуску на 'Never'. | ![](/yaml/app-configmap.yaml) |