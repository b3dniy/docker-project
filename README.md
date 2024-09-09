1. Мониторинг (Prometheus):
Контейнер с образом prom/prometheus был добавлен для отслеживания состояния удаленных сервисов.
Порты:
Контейнер на порту 9090, что позволяет доступ к веб-интерфейсу Prometheus через локальный хост (localhost).
Файл конфигурации Prometheus (prometheus.yml) был смонтирован как volume, чтобы он мог загружать настройки мониторинга из указанного файла.
Конфигурация:

В Docker Compose используется образ Prometheus, который монтирует конфигурационный файл Prometheus в контейнер для отслеживания метрик. Мониторинг работает через порт 9090, который проброшен на хост для доступа к веб-интерфейсу мониторинга.
2. DNS (Pi-hole):
Контейнер с образом pihole/pihole был настроен как DNS-сервер для возврата правильных IP-адресов выбранного сервиса.
Порты:
Контейнер использует порты 53/udp и 53/tcp для работы DNS.
Переменные окружения для DNS-сервера установлены:
DNS1=8.8.8.8 (Google DNS).
DNS2=8.8.4.4.
Установлен пароль для веб-интерфейса WEBPASSWORD=kozlovAD123.
Конфигурация:

DNS-сервер настраивается через образ Pi-hole, который используется для кеширования DNS-запросов и блокировки рекламы. Конфигурация DNS через Google (8.8.8.8 и 8.8.4.4) была установлена как первичные и вторичные DNS-серверы, а веб-интерфейс можно было бы доступить через пароль.
3. Выбранный сервис (WordPress):
Контейнер с образом wordpress был настроен как выбранный веб-сервис для разворачивания сайта.
Порты:
Контейнер проброшен на порт 8080:80, что позволяет доступ к WordPress через локальный хост на порте 8080.
База данных MySQL настроена отдельно с помощью контейнера с образом mysql:5.7.
Переменные окружения установлены для взаимодействия с базой данных:
WORDPRESS_DB_HOST: Имя хоста базы данных db.
WORDPRESS_DB_USER: Имя пользователя базы данных kozlovAD.
WORDPRESS_DB_PASSWORD: Пароль для базы данных kozlovAD123.
WORDPRESS_DB_NAME: Имя базы данных kozlovADdb.
Конфигурация:

WordPress настроен с отдельной базой данных MySQL. Порт 8080 проброшен для доступа к сайту. Данные для подключения WordPress к базе данных настроены через переменные окружения. База данных MySQL хранит информацию о сайте WordPress.
4. Сеть (mynetwork):
Все сервисы подключены к пользовательской сети mynetwork, которая использует драйвер bridge. Это обеспечивает общение между контейнерами.
Дополнительно:
Было проведено тестирование корректности работы DNS и выбранного сервиса, подтверждено, что DNS-сервер отвечает на запросы, а WordPress доступен через браузер.
