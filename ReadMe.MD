# DWH
Практическое задание для магистров


## Результат

Выполнено 8 и 9 задание. Реализована загрузка данных в Spark и их последующая обработка в DWH и показ на витрине. 
Реализован обновление данных при изменении данных в источнике. 

К сожалению, на витрине обновляется целиком, а не одной записью. 

### Как запустить

1. Запустить docker compose
2. http://127.0.0.1:8888/lab
3. Запустить run.ipynb


### Идея: Маркетплейс товаров ручного производства из разных стран.

Вы работаете в компании, которая создает приложение маркетплейс для эксклюзивных товаров ручной работы мастеров. Мастера, которые изготавливают свои товары вручную выкладывают их на продажу на различных сайтах, у каждого из которых свой бэкенд со своей моделью данных в БД. Ваша компания покупает эти сайты, но не меняет у них домены, а значит, мастера всё ещё могут туда выкладывать свои товары, а покупатели делать там покупки. Нужно организовать корпоративное хранилище данных (DWH) на основе данных из трех источников и построить конечную витрину данных со статистикой о продажах.

Алгоритм решения задания:
1. Установить себе Docker Desktop - https://www.docker.com/products/docker-desktop/ 
2. Установить себе DBeaver Community - https://dbeaver.io/
3. Запустить в docker СУБД PostgrSQL
   - https://habr.com/ru/articles/823816/
   - https://habr.com/ru/articles/578744/
   - https://www.docker.com/blog/how-to-use-the-postgres-docker-official-image/
   - https://geshan.com.np/blog/2021/12/docker-postgres/
   - https://hub.docker.com/_/postgres
4. Запустить DBeaver и с помощью скриптов из папки "Cкрипты создания таблиц источников" - создать пустые таблицы источников в PostgreSQL
5. С помощью DBeaver импортировать данные из csv файлов в папке "Данные для источников" в пустые таблицы, созданные на предыдущем шаге
6. С помощью DBeaver запустить скрипты из папки "Скрипты по созданию таблиц DWH и витрин". Скрипты создадут таблицы фактов, измерений и таблицы для витрины данных.
7. Запустите Spark в Docker, чтобы он имел доступ к PostgreSQL в docker (нужно настроить сетевую связанность между ними)
   - https://hub.docker.com/r/jupyter/all-spark-notebook
   - https://stackoverflow.com/questions/37694987/connecting-to-postgresql-in-a-docker-container-from-outside
8. Напишите код на Spark, который будет заполнять сначала таблицы измерений и фактов в DWH.
   - https://spark.apache.org/docs/latest/sql-getting-started.html
   - https://spark.apache.org/docs/3.5.1/sql-data-sources-jdbc.html
9. Затем напишите код на Spark, который заполнит таблицу витрины данных из данных таблиц измерений и фактов в DWH. Напишите код инкрементальным, чтобы можно было забирать только измененные данные на источниках.
   - https://spark.apache.org/docs/latest/sql-getting-started.html
   - Обратите внимание на комментарии к колонкам в скрипте DDL витрины данных dwh.craftsman_report_datamart. Там написано, что должно содержаться в этих колонках.

Общая схема задания
![Сквозной кейс схема](https://github.com/user-attachments/assets/3d057216-7b96-4bca-a75e-83f3ea5d9696)


# Как сдавать задание:

Минимальные требования для сдачи практической работы:
1. Должен быть ваш репозиторий с кодом на Apache Spark - его надо прислать в тг @neltari.
2. PostgreSQL и Spark должны запускаться в Docker.
3. В Readme репозитория должна быть инструкция, как запускать скрипты для проверки.
4. Должна быть реализована инкрементальная загрузка
