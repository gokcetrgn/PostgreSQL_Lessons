# PostgreSQL_Lessons

Bu repo'da dvdrental adlı hazır bir veritabanı kullanılmıştır. dvdrental adlı veritabanından film tablosu çekilmiştir. Sorgular ona aittir

Kullanılabilecek kaynaklar:

[W3Schools](https://www.w3schools.com/sql/sql_select.asp) & [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)


# SQL Ödev 1:

- film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```
-- SELECT column1 FROM table1;

-- Sorguların büyük harfli olması karışıklığı önler:

SELECT title,description FROM film;
```

# SQL Ödev 2:

- film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.
  
