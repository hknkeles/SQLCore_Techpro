---
tags:
  - SQL
  - pratikler
aliases:
  - techpro
  - pratik
---
# 📖 ÖDEV 1 
<hr>


## 1-sqlpractice_db isminde database oluşturunuz. Butun odevleri bu db icinde cozunuz

```sql
CREATE DATABASE sqlpractice_db;
```
​
## 2-sqlpractice_db database içinde musteri isminde tablo oluşturunuz.​

> [!FAQ]
>   musteri_no(integer) 
>   isim (string,50 karakter)
>   yas (int)
>   cinsiyet (string 1 karakter)
>   gelir(real)
>   meslek(string,20 karakter)
>   sehir (string,20 karakter)
​
> [!warning] **Constraintler**
> musteri_no: primary key, otomatik olarak artırılsın​
> isim: not null ve not empty,
> yas:18 den büyük

```sql
​ CREATE TABLE musteri(
	musteri_no SERIAL PRIMARY KEY,
	isim VARCHAR(50) NOT NULL CHECK(isim!=''),
	yas INTEGER CHECK(yas>18),
	gelir REAL,
	meslek VARCHAR(20),
	sehir VARCHAR(20)
 );
 
 SELECT * FROM musteri;
```

## 3-musteri tablosuna kayıt ekleyiniz.​

```sql
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('Ali',     35,'E',  2500, 'MÜHENDİS',    'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('CEYHUN',  45, 'E', 2000, 'MÜHENDİS',    'ANKARA');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('DEMET',   30, 'K', 3000, 'ÖĞRETMEN',    'ANKARA');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('FERHAT',  40, 'E', 2500, 'MİMAR',       'İZMİR');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('GALİP',   55, 'E', 4000, 'ÖĞRETMEN',    'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('KÖKSAL',  25, 'E', 2000, 'AVUKAT',      'İZMİR');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('LEYLA',   60, 'K', 2500, 'MİMAR',       'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('MELEK',   30, 'K', 2500, 'ÖĞRETMEN',    'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('JALE',    40, 'K', 6000, 'İŞLETMECİ',   'ANKARA');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('TEKİN',   45, 'E', 2000, 'AVUKAT',      'ANKARA');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('SAMET',   20, 'E', 3000, 'MİMAR',       'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('ŞULE',    20, 'K', 4500, 'ÖĞRETMEN',    'İSTANBUL');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('VELİ',    40, 'E', 2500, 'ÖĞRETMEN',    'İZMİR');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('ZEYNEP',  50, 'K', 3500, 'TESİSATÇI',   'İZMİR');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('ARDA',    55, 'E', 2000, 'KUAFÖR',      'İZMİR');
INSERT INTO musteri(isim,yas,cinsiyet,gelir,meslek,sehir) VALUES('MELİS',   30, 'K', 3000, 'KUAFÖR',      'ANKARA');
```


## ​**Musteri tablosunda;**
## 4- Tüm kayıtları listeleyiniz.
​
```sql
SELECT * FROM musteri;
```
## 5-Tüm kayıtlardan isim ve meslek bilgilerini görüntüleyiniz
​
```sql
SELECT isim, meslek FROM musteri;
```

## 6-sqlpractice_db database'inde “sehirler” isimli bir Table olusturun. ​

> [!warning] Dikkat
> Tabloda “alan_kodu”, “isim”, “nufus”  field’lari olsun.​
> 
> Isim field’i null değer alamasın.​
> 
> “alan_kodu” field’ini “Primary Key” yapin.


``` sql
CREATE TABLE sehirler(
	alan_kodu INTEGER PRIMARY KEY,
	isim VARCHAR(50) NOT NULL,
	nufus INTEGER
); 

SELECT * FROM sehirler;
```

## 7-sqlpractice_db database'inde;​
### a- “tedarikciler3” isimli bir tablo olusturun.
​

> [!warning] Dikkat
> Tabloda “tedarikci_id”, “tedarikci_ismi”,  “iletisim_isim” field’lari olsun ​
> 
> “iletisim_isim”  fieldı tekrarsız olsun.> ​
> 
> “tedarikci_id” yi Primary Key yapin.
> 

```sql
CREATE TABLE tedarikciler3(
	tedarikci_id SERIAL PRIMARY KEY,
	tedarikci_ismi VARCHAR(50),
	iletisim_isim VARCHAR(50) UNIQUE
);

SELECT * FROM tedarikciler3;
```
​
### b- “urunler” isminde baska bir tablo olusturun “tedarikci_id” ve “urun_id” field’lari olsun​

> [!warning] Dikkat
> “tedarikci_id” yi Foreign Key yapin.


```sql
CREATE TABLE urunler(
	urun_id SERIAL PRIMARY KEY,
	tedarikci_id INTEGER,
	CONSTRAINT fk_tedarikci_id FOREIGN KEY(tedarikci_id) REFERENCES tedarikciler3(tedarikci_id)
);
```

---
# 📖 <font color="#245bdb">ÖDEV 2 </font>
<hr>


## 1) Tablo Oluşturma

​filmler isminde bir tablo oluşturunuz.

> [!warning] Dikkat
> film_isim(varchar(50)), tür(varchar(20)), 
> 
> süre(real), imdb(numeric(2,1)) 
> 
> sütunları olsun. 



​
## 2)  Data ekleme

### a-filmler tablosuna tüm fieldlarıyla 3 tane kayıt ekleyiniz.



### b- “ogretmenler” isminde tablo olusturun.

İçinde “kimlik_no”, “isim”, “brans” ve “cinsiyet” field’lari olsun
**(uygun data tiplerini kullanınız.)**

> [!NOTE]
> **“ogretmenler” tablosuna bilgileri asagidaki gibi olan kisileri ekleyin.**
> 
> kimlik_no: 234431223, isim: Ayse Guler, brans : Matematik, cinsiyet: kadin.
> 
> kimlik_no: 234431224, isim: Ali Guler, brans : Fizik, cinsiyet: erkek.
> 

### ​3) Var olan tablodan yeni tablo oluşturmak 

> [!NOTE]
>  “film_imdb” isminde bir tabloyu  “filmler” tablosundan oluşturunuz.
> 
> İçinde “film_isim” ve “imdb” field’lari olsun
### 4) Bazı fieldları olan kayıt ekleme

### a-"filmler" tablosuna 

> [!NOTE]
> film_isim:"Ayla", “film_imdb”:9.87,
> 
> film_isim:"Shrek", “film_imdb”:9.83
> 
> olan kayıtları ekleyiniz.
### b-“ogretmenler” tablosuna bilgileri 

> [!NOTE]
> kimlik_no: 567597624, isim: Veli Guler
> 
> olan kişiyi ekleyiniz.

