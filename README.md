# PostgreSQL_Lessons

Bu repo'da dvdrental adlı hazır bir veritabanı kullanılmıştır. dvdrental adlı veritabanından film tablosu çekilmiştir. Sorgular ona aittir

Kullanılabilecek kaynaklar:

[W3Schools](https://www.w3schools.com/sql/sql_select.asp) & [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)

Hazır veri eklemek icin:

[Random Data Generator](https://www.mockaroo.com/)


# SQL Ödev 1:

- film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```
-- SELECT column1 FROM table1;

-- Sorguların büyük harfli olması karışıklığı önler:

SELECT title,description FROM film;
```
- film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.
```
SELECT * FROM film
WHERE (length > 60 AND length < 75);

-- * kullanmak verilerin geri dönüşünü uzattığı icin ihtiyacımız olan sütunları çağırırız.
-- from'dan sonra bir alt satıra geçilerek kodun daha iyi anlaşılması hedeflenir.
```

- film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.
```
SELECT * FROM film
WHERE (rental_rate = 0.99 AND replacement_cost = 12.99 OR replacement_cost = 28.99);
```

- customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?
```
SELECT first_name, last_name FROM customer
WHERE first_name = 'Mary';

Çıktı: Smith
```
- film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.
```
SELECT * FROM film
WHERE length < 50 AND NOT (rental_rate = 2.99 OR rental_rate = 4.99);
```

# SQL Ödev 2:
- film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)
```
SELECT * FROM film
WHERE replacement_cost BETWEEN 12.99 AND 16.99;
```
- actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)
```
SELECT first_name, last_name FROM actor
WHERE first_name IN('Penelope','Nick','Ed');
```
- film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)
```
SELECT * FROM film
WHERE (rental_rate IN(0.99,2.99,4.99)) AND (replacement_cost IN(12.99,15.99,28.99));
```

# SQL Ödev 3:
- country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.
```
-- LIKE 'M%' 'daki % işareti yer tutucu işlevi görür.
-- Büyük harf küçük harf dikkat etmesin istiyorsak ILIKE
-- 'M____' yaparsak 4 harf için tutuculuk yapar.
-- ~~ koyulursa LIKE ~~* koyulursa ILIKE yerine geçer.

SELECT country FROM country
WHERE country ~~ 'A%a';

```

- country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.
```
SELECT country FROM country
WHERE country LIKE '______%n';
```

- film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.
```
SELECT title FROM film
WHERE title ILIKE '%t%t%t%t';
```
- film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.
```
SELECT * FROM film
WHERE title LIKE 'C%' AND length > 90 AND rental_rate = 2.99;
```

# SQL Ödev 4:

- film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.
```
SELECT DISTINCT replacement_cost FROM film;
```
- film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?
```
SELECT COUNT(DISTINCT replacement_cost) FROM film;
Çıktı : 21
```
- film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?
```
SELECT COUNT(title) FROM film
WHERE title LIKE 'T%' AND rating = 'G';

Çıktı: 9
```
- country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?
```
SELECT COUNT(DISTINCT country) FROM country
WHERE country LIKE '_____';

Çıktı: 13
```
- city tablosundaki şehir isimlerinin kaç tanesi 'R' veya r karakteri ile biter?
```
SELECT COUNT(DISTINCT city) FROM city
WHERE city ILIKE '%R';

Çıktı: 33
```
# SQL Ödev 5:
- film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.
```
SELECT * FROM film
WHERE title ILIKE '%n'
ORDER BY length DESC
LIMIT 5;
```
- film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.
```
SELECT * FROM film
WHERE title ILIKE '%N'
ORDER BY length ASC
OFFSET 5
LIMIT 5;
```
- customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.
```
SELECT * FROM customer
WHERE store_id = 1
ORDER BY last_name DESC
LIMIT 4;
```
# SQL Ödev 6:
- film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?
```
SELECT ROUND(AVG(rental_rate), 3) from film;

Çıktı: 2.980
```
- film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?
```
SELECT COUNT(*) FROM film
WHERE title LIKE 'C%';

Çıktı: 92
```
- film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?
```
SELECT MAX(length) FROM film
WHERE rental_rate = 0.99;

Çıktı: 184
```
- film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?
```
SELECT COUNT(DISTINCT replacement_cost) FROM film
WHERE length > 150;

Çıktı: 21
```

# SQL Ödev 7

- film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.
```
SELECT rating, COUNT(*) FROM film
GROUP BY rating;
```

- film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.
```
SELECT replacement_cost, COUNT(*) FROM film
GROUP BY replacement_cost
HAVING COUNT(*) > 50;;
```

- customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir?
```
SELECT store_id, COUNT(*) FROM customer
GROUP BY store_id
```
- city tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.
```
SELECT country_id, COUNT(*) FROM city
GROUP BY country_id
ORDER BY COUNT(*) DESC
LIMIT 1;
```
# SQL Ödev 8
- test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.
```
-- CREATE TABLE <tablo_adı> (
--   <sütun_adı> <veri_tip> (kısıtlama_adı>,
--   <sütun_adı> <veri_tip> (kısıtlama_adı>,
--   ....
-- );

CREATE TABLE employee (
  id int PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  birthday DATE,
  email VARCHAR(100)
);
```
- Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
```
insert into employee (id, name, email, birthday) values (1, 'Lorena', 'lcalderhead0@un.org', null);
insert into employee (id, name, email, birthday) values (2, 'Manda', 'mkisby1@alibaba.com', '1945-12-03');
insert into employee (id, name, email, birthday) values (3, 'Lyndsie', 'lkeggin2@google.ca', '1974-09-28');
insert into employee (id, name, email, birthday) values (4, 'Pammie', 'pneedham3@dell.com', '1987-07-04');
insert into employee (id, name, email, birthday) values (5, 'Orelie', 'ooneill4@europa.eu', '1982-08-21');
insert into employee (id, name, email, birthday) values (6, 'Bourke', 'bcrain5@photobucket.com', '1953-01-06');
insert into employee (id, name, email, birthday) values (7, 'Tully', 'tvasse6@wiley.com', null);
insert into employee (id, name, email, birthday) values (8, 'Carr', 'cjosiah7@yelp.com', '1962-11-21');
insert into employee (id, name, email, birthday) values (9, 'Andros', 'aloblie8@skype.com', '1973-11-03');
insert into employee (id, name, email, birthday) values (10, 'Ulrich', 'uschwieso9@mysql.com', null);
insert into employee (id, name, email, birthday) values (11, 'Sharyl', 'svereckera@loc.gov', '1931-01-07');
insert into employee (id, name, email, birthday) values (12, 'Nixie', 'nvaughanb@flavors.me', '1978-06-15');
insert into employee (id, name, email, birthday) values (13, 'Tildy', 'ttoulminc@php.net', '1935-05-04');
insert into employee (id, name, email, birthday) values (14, 'Kenyon', 'kspeedd@ehow.com', null);
insert into employee (id, name, email, birthday) values (15, 'Ericha', 'ealowaye@hao123.com', '1972-02-20');
insert into employee (id, name, email, birthday) values (16, 'Taddeusz', 'tpyburnf@plala.or.jp', '1926-03-11');
insert into employee (id, name, email, birthday) values (17, 'Chandra', 'cmacgiollapheadairg@myspace.com', '1961-12-16');
insert into employee (id, name, email, birthday) values (18, 'Enrica', 'eharrieh@irs.gov', '1918-11-17');
insert into employee (id, name, email, birthday) values (19, 'Ruperto', null, '1915-08-21');
insert into employee (id, name, email, birthday) values (20, 'Meridith', null, null);
insert into employee (id, name, email, birthday) values (21, 'Eddie', 'efritterk@latimes.com', '1978-10-26');
insert into employee (id, name, email, birthday) values (22, 'Terrell', 'tmccaddenl@ustream.tv', '1955-05-01');
insert into employee (id, name, email, birthday) values (23, 'Birgitta', 'bfarrierm@hao123.com', '1958-10-07');
insert into employee (id, name, email, birthday) values (24, 'Chase', null, '1977-05-06');
insert into employee (id, name, email, birthday) values (25, 'Gwenny', 'gfountiano@mail.ru', '1916-11-10');
insert into employee (id, name, email, birthday) values (26, 'Niki', 'nfraulop@edublogs.org', '1972-06-03');
insert into employee (id, name, email, birthday) values (27, 'Billie', 'bklulisekq@histats.com', null);
insert into employee (id, name, email, birthday) values (28, 'Amie', 'ahuertasr@bizjournals.com', null);
insert into employee (id, name, email, birthday) values (29, 'Bondon', 'briverss@homestead.com', null);
insert into employee (id, name, email, birthday) values (30, 'Elisabet', 'ehixsont@amazonaws.com', '1963-10-24');
insert into employee (id, name, email, birthday) values (31, 'Viki', 'vdibleu@people.com.cn', '1964-04-30');
insert into employee (id, name, email, birthday) values (32, 'Rickert', 'rrobinetv@mashable.com', null);
insert into employee (id, name, email, birthday) values (33, 'Amos', 'ahaggettw@dedecms.com', null);
insert into employee (id, name, email, birthday) values (34, 'Gerry', 'gmcpharlainx@irs.gov', '1936-08-12');
insert into employee (id, name, email, birthday) values (35, 'Saunderson', 'smccracheny@ifeng.com', null);
insert into employee (id, name, email, birthday) values (36, 'Blinni', 'bswadlingz@admin.ch', '1971-11-08');
insert into employee (id, name, email, birthday) values (37, 'Merell', null, '1927-08-21');
insert into employee (id, name, email, birthday) values (38, 'Lesly', 'lfawltey11@t-online.de', null);
insert into employee (id, name, email, birthday) values (39, 'Yolanda', 'yrose12@fda.gov', '1937-05-10');
insert into employee (id, name, email, birthday) values (40, 'Elmer', 'ecaven13@deviantart.com', null);
insert into employee (id, name, email, birthday) values (41, 'Katherina', 'kdillet14@eepurl.com', null);
insert into employee (id, name, email, birthday) values (42, 'Fawne', 'fpires15@mozilla.org', '1940-08-21');
insert into employee (id, name, email, birthday) values (43, 'Lily', 'ldemars16@deviantart.com', null);
insert into employee (id, name, email, birthday) values (44, 'Leonidas', 'lwilloughby17@pagesperso-orange.fr', '1940-12-04');
insert into employee (id, name, email, birthday) values (45, 'Linet', 'ltaffurelli18@loc.gov', '1959-11-29');
insert into employee (id, name, email, birthday) values (46, 'Granville', 'glongland19@go.com', '1944-12-29');
insert into employee (id, name, email, birthday) values (47, 'Melisse', 'mhayden1a@dropbox.com', '1982-03-23');
insert into employee (id, name, email, birthday) values (48, 'Cacilia', 'ccathie1b@360.cn', '1926-03-30');
insert into employee (id, name, email, birthday) values (49, 'Husain', 'hchatan1c@t-online.de', '1992-11-15');
insert into employee (id, name, email, birthday) values (50, 'Boyd', 'bguinane1d@is.gd', '1916-09-23');
```
- Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.
```
UPDATE employee
SET name = 'Malik',
    email = 'malik@gmail.com' // isim-email güncelleme
WHERE id = 45;

UPDATE employee
SET name = 'Emily', // isim güncelleme
WHERE id = 46;

UPDATE employee
SET email = 'jeniffer@gmail.com' // email güncelleme
WHERE id = 47;

UPDATE employee
SET birthday = '1988-12-14' // birthday güncelleme
WHERE id = 48;

UPDATE employee
SET name = 'Selly',
    email = 'sellyshhw@gmail.com'
    birthday = '2003-05-29' // isim-email-birthday güncelleme
WHERE id = 49;
```
- Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.
```
DELETE FROM employee
WHERE name = 'Malik';

DELETE FROM employee
WHERE id = 44;

DELETE FROM employee
WHERE email = 'ldemars16@deviantart.com';

DELETE FROM employee
WHERE birthday = '1940-08-21';

DELETE FROM employee
WHERE id > 45
RETURNING *;
```

# SQL Ödev 9

- city tablosu ile country tablosunda bulunan şehir (city) ve ülke (country) isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
SELECT city.city, country.country FROM country
JOIN city ON city.country_id = country.country_id;
```

- customer tablosu ile payment tablosunda bulunan payment_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
SELECT payment.payment_id, customer.first_name, customer.last_name FROM customer
JOIN payment ON payment.customer_id = customer.customer_id;
```
- customer tablosu ile rental tablosunda bulunan rental_id ile customer tablosundaki first_name ve last_name isimlerini birlikte görebileceğimiz INNER JOIN sorgusunu yazınız.
```
SELECT rental.rental_id, customer.first_name, customer.last_name FROM customer
INNER JOIN rental ON rental.customer_id = customer.customer_id;
```
