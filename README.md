# API YaMDb
Проект YaMDb собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

## Стек технологий
* Python 3.9.1, 
* Django 3.0.5, 
* Django REST Framework, 
* SQLite3, 
* Simple JWT, 
* Django Filter.

## Установка
Создайте виртуальное окружение:
```python
python -m venv venv
```

Активируйте его:
```python
source venv/Scripts/activate
```

Используйте [pip](https://pip.pypa.io/en/stable/), чтобы установить зависимости:
```python
pip install -r requirements.txt
```

После создайте в корневой директории файл с названием ".env" и поместите в него:
```python
SECRET_KEY=любой_секретный_ключ_на_ваш_выбор
DEBUG=False
ALLOWED_HOSTS=*
```
Не забудьте применить все миграции:
```python
python manage.py migrate
```

И запускайте сервер:
```python
python manage.py runserver
```

## Как импортировать дату в базу данных?
Используйте shell:

``` python manage.py shell ```

Импортируйте скрипт:
```python
from data.import_data import import_data
```

Запустите скрипт:
* Если вам нужен отчёт о каждой ошибке:
```python
import_data(True)
```

* Если не нужен:
```python
import_data()
```

## Как импортировать дату из своего csv файла?
1. Заходим в shell:
```python
python manage.py shell
```

2. Импортируем нужные модели:
```python
from api.models import User, Category, Comment, Genre, Review, Title
```

3. Импортируем скрипт:
```python
from data.import_data import create_models
```

4. Запускаем скрипт с тремя параметрами:

file_path — путь до вашего csv файла,

model — класс модели из импортированных ранее,

print_errors — нужно ли распечатать каждую ошибку подробно? (True or False)

Пример:

```python
create_models('data/review.csv', Review, False)
``` 

## Вход
Создайте супер пользователя, обязательно укажите почту и пароль:

```python
python manage.py createsuperuser
```

Отправьте POST-запрос на ссылку: http://127.0.0.1:8000/api/v1/auth/email/ — не забудьте указать в параметрах вашу почту! Пример:

```python
curl -X POST -F "email=ваша_почта@gmail.com" http://127.0.0.1:8000/api/v1/auth/email/
```

В папке ./sent_emails/ появится новое "письмо", откройте его и скопируйте код для авторизации.

Теперь отправьте POST-запрос, только с кодом на http://127.0.0.1:8000/api/v1/auth/token/, чтобы получить токен. Пример:

```python
curl -X POST -F "email=ваша_почта@gmail.com" -F "confirmation_code=ваш_код" http://127.0.0.1:8000/api/v1/auth/token/
```

Документация
Чтобы открыть документацию, запустите сервер и перейдите по ссылке: http://127.0.0.1:8000/redoc/
