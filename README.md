# Переменные среды

### TEST_LEVEL

Уровень сдаваемой задачи. Допустимые значения: 1, 2, 3.

- Уровень 1 - проверка математики
- Уровень 2 - к уровню 1 добавляется длинная арифметика
- Уровень 3 - к уровню 2 добавляется некорректный ввод и ввод комплЕксных чисел

# Разработка

В директории `source` можно писать код. Название проекта в CMakeLists.txt лучше не менять, а то тесты работать не будут.

# Запуск

0. Установить Docker, рекомендую [Docker Desktop](https://www.docker.com/products/docker-desktop/)

1. Скопировать `.env.example` в `.env`

```bash
cp .env.example .env
```

2. Задать переменную `TEST_LEVEL` в файле `.env`

3. Запустить контейнер:

```bash
docker compose up --build
```

# Как работает тестовая система

При запуске контейнера сначала с помощью cmake собирается проект. Далее для собранного приложения запускаются тесты.

В зависимости от указанного `TEST_LEVEL` запускаются все тесты от 1 уровня до `TEST_LEVEL`.

Если уровень пройден, то будет выведено:

```
Running test level #1
All tests passed
```

Если произошла ошибка во время тестирования, то будет выведена информация о ней:

```
Running test level #1

##########
Test #2 failed: Wrong answer
Input: '1 2 1'
Details:
Root mismatch: got '1', expected one of [-1, -1]
##########
```

### Виды ошибок:

- Runtime error - в вашей программе произошла ошибка во время выполнения
- Time limit error - превышено ограничение выполнения программы по времени
- Memory limit error - превышено ограничение выполнения программы по оперативной памяти
- Wrong answer - получен неправильный ответ на тест (в том числе возникает из-за неправильного формата вывода)
