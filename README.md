# Проект на Spring Framework з підтримкою системи Трембіта

## Опис
Цей проєкт входить в набір прикладів взаємодії з API шлюзу безпечного обміну системи Трембіта (ШБО), що демонструють технічні особливості розробки вебсервісів та вебклієнтів, сумісних з системою Трембіта.
Даний проєкт представляє опис створення сумісного REST-сервісу на мові програмування Java з використанням фрейморка Spring. Spring - це сучасний, швидкий (високопродуктивний) фреймворк для Java.\
Приклад описує отримання з умовної бази даних (реєстру) відомостей про інформаційні об'єкти (у прикладі об'єктом є користувач) та управління їх статусом, у тому числі обробку запитів на пошук, отримання, створення, редагування та видалення об'єктів через REST API, що доступне через систему Трембіта.\
Проєкт демонструє:
- Cтандартні синхронні та асинхронні виклики
- Роботу з БД PostgreSQL (функції додавання, пошуку, оновлення та видалення об'єктів)
- Логування роботу застосунку з налаштуванням деталізації
- Роботу з файлом конфігурації
- Створення опису API за допомогою Swagger
- Підтримку системи Трембіта (логування заголовків).

## Вимоги
- Java 17+
- Git (для клонування репозиторію)
- PostgreSQL 14.12
- Ubuntu Server 22.04

## Встановлення

### Встановлення за допомогою скрипта install_SpringWS.sh

Було створено скрипт `install_SpringWS.sh` для автоматизації процесу встановлення середовища розробки, готового до компіляції прикладу. Скрипт виконує наступні кроки:
1. Встановлює системні залежності.
2. Клонує репозиторій.
3. Встановлює або оновлює Java 21.
4. Встановлює та налаштовує базу даних PostgreSQL 14.12.
5. Завантажує та налаштовує середовище розробки Apache NetBeans 19.

#### Використання скрипта install_SpringWS.sh

На вашій робочій станції для розробки виконайте наступні кроки:
1. Завантажте скрипт `install_SpringWS.sh` в папку Documents
2. Зробіть файл виконуваним:

   ```bash
   sudo chmod +x install_SpringWS.sh
   ```

3. Запустіть скрипт:

   ```bash
   sudo bash ./install_SpringWS.sh
   ```
4. Надайте відповідь на запитання скрипту щодо імені бази даних, яка буде використовуватись для проєкту, імені користувача бази даних, пароля користувача БД (Скрипт сам створить БД, створить роль та встановить вказаний вами пароль).

5. В деяких випадках скрипт може пропонувати перезавантажити деякі системні служби - просто натисніть Enter.

6. Після того як виконання скрипту буде завершено, запустіть середовище розробки Apache NetBeans, та виконайте індексування репозіторію Maven. Для цього:
  - 6.1. В середовищі розробки (IDE) Apache NetBeans натисніть меню Tools->Options
  - 6.2. У вікні, що відкриється, натисніть пункт Java
  - 6.3. У панелі вкладок нижче перейдіть на вкладку Maven 
  - 6.4. Виберіть пункт Index в меню ліворуч
  - 6.5. Після чого натисніть кнопку Index Now
  - 6.6. Зачекайте доки індексування репозіторію буде завершено, після чого можно відкривати проект (може зайняти кілька хвилин).

### Ручне встановлення

#### Оновлення списку доступних пакетів програмного забезпечення з офіційних репозиторіїв 

```bash
sudo apt update
```

#### Встановлення Java JDK 21

```bash
sudo apt install openjdk-21-jdk 
```

#### Створення БД. Цей сервіс використовує PostgreSQL. Створіть базу даних та користувача на сервері СКБД.

```bash
sudo apt install postgresql postgresql-contrib
```

#### Налашування бази даних PostgreSQL

```bash
sudo -i -u postgres psql
```
CREATE DATABASE dbname;

CREATE ROLE dbusername LOGIN PASSWORD 'dbuserpassword';

GRANT ALL PRIVILEGES ON DATABASE dbname TO dbusername;

Для вихода з командного рядку БД psql введіть \q

#### Завантажити та встановити середовище розробки Apache NetBeans ви можете через браузер, або через додаток Ubuntu Software

#### Завантажити Github клієнт

```bash
sudo apt install git
```
#### Отримаємо та запам'ятаємо ім'я поточного користувача

```bash
whoami
```
#### Клонування репозиторію

```bash
git clone https://github.com/Wishmaster-sa/SpringWS.git

sudo mv ./SpringWS/maven ./SpringWS/.mvn

cd SpringWS
```
```bash
sudo bash mvnw -N wrapper:wrapper
```


#### Подальші дії: Запустіть середовище розробки Apache NetBeans, та виконайте індексування репозіторію Maven. Для цього:
   
   1. В середовищі розробки (IDE) Apache NetBeans натисніть меню Tools->Options
   2. У вікні що відкрилося натисніть пункт Java
   3. У панелі вкладок нижче перейдіть на вкладку Maven 
   4. Виберіть пункт Index в меню ліворуч
   5. Після чого натисніть кнопку Index Now
   6. Зачекайте доки індексування репозіторію буде завершено, після чого можно відкривати проект (може зайняти кілька хвилин).

#### Налаштування підключення до БД в проєкті

Відкрити файл конфігурації застосунку Spring './SpringWS/src/main/resources/application.properties' та встановити коректні параметри підключення до БД - ім'я бази, ім'я та пароль користувача згідно значень, заданих на кроці налаштування бази даних PostgreSQL. Наприклад:
```
spring.datasource.url=jdbc:postgresql://localhost:5432/dbname
spring.datasource.username=dbusername
spring.datasource.password=dbuserpassword
```

### Запуск сервісу


```bash
java -jar ./target/SpringWS-0.0.1-SNAPSHOT.jar
```

Сервіс запуститься і буде очікувати на вхідні мережеві з'єднання на порту 8080 за адресою
http://localhost:8080/

Тут `SpringWS-0.0.1-SNAPSHOT.jar` - це ім'я скомпільованого файлу проєкту. Відкрийте браузер і перейдіть за адресою http://[адреса серверу]:8080.


## Документація

Після запуску сервісу ви можете отримати доступ до автоматичної документації API за наступними адресами:

- Doc: http://[адреса серверу]:8080/
- Swagger UI: http://[адреса серверу]:8080/swagger-ui/index.html

## Наповнення бази даних тестовими записами
Для цілей швидкого розгортання та використання сервісу ми додаємо Python-скрипт, який дозволяє швидко згенерувати
необхідну кількість записів в БД.
   ```python
   python fill_fakerdb.py 100
   ```
де 100 - кількість об'єктів (користувачів), яка буде згенерована та додана до БД. Ви можете встановити іншу кількість записів.

## Налаштування як системної служби systemd

Для цілей швидкого запуску сервісу ми додаємо скрипт `springws-service.sh` для автоматизації процесу встановленя веб-додатка як системної служби, та його видалення та очищення системи.

### Використання скрипта springws-service.sh
1. Скомпілюйте через середовище розробки та скопіюйте jar-файл веб-сервісу до цільової системи.
   Ви повинні отримати в папці SpringWS/target/SpringWS-0.0.1-SNAPSHOT.jar скомпільований jar-файл 

2. Зробіть скріпт виконуваним:

   ```bash
   chmod +x springws-service.sh
   ```

3. Запустіть скрипт з каталогу SpringWS:

   ```bash
   ./springws-service.sh install
   ```

Скрипт автоматично вcтановить скомпільований jar як системну службу.

Якщо ви бажаєте видалити сервіс з переліку системних служб, то виконайте команду
   ```bash
   ./springws-service.sh remove
   ```
Скрипт автоматично зупинить та видалить системну службу та відповідні залежності.

Запустити сервіс
   ```bash
   ./springws-service.sh start
   ```
Припинити сервіс
   ```bash
   ./springws-service.sh stop
   ```
Якщо ви виконаєте файл без аргументів командного рядку, то вам буде запропоновано меню з наступними опціями:
1) Встановити сервіс
2) Запустити сервіс
3) Припинити сервіс
4) Видалити сервіс
5) Вихід

## Ліцензія

Цей проєкт ліцензується відповідно до умов MIT License.
