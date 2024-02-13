SELECT *
FROM products;

1. Product isimlerini (`ProductName`) ve birim başına miktar (`QuantityPerUnit`) değerlerini almak için sorgu yazın.
```sql
SELECT product_name, quantity_per_unit
FROM products;
```

2. Ürün Numaralarını (`ProductID`) ve Product isimlerini (`ProductName`) değerlerini almak için sorgu yazın. Artık satılmayan ürünleri (`Discontinued`) filtreleyiniz.
```sql
SELECT product_id, product_name
FROM products
WHERE discontinued=0;
```

3. Durdurulan (`Discontinued`) Ürün Listesini, Ürün kimliği ve ismi (`ProductID`, `ProductName`) değerleriyle almak için bir sorgu yazın.
```sql
SELECT product_id, product_name
FROM products
WHERE discontinued=1;
```

4. Ürünlerin maliyeti 20'dan az olan Ürün listesini (`ProductID`, `ProductName`, `UnitPrice`) almak için bir sorgu yazın.
```sql
SELECT product_id, product_name, unit_price
FROM products
WHERE unit_price < 20;
```

5. Ürünlerin maliyetinin 15 ile 25 arasında olduğu Ürün listesini (`ProductID`, `ProductName`, `UnitPrice`) almak için bir sorgu yazın.
```sql
SELECT product_id, product_name, unit_price
FROM products
WHERE unit_price < 25 AND unit_price > 15;
```

6. Ürün listesinin (`ProductName`, `UnitsOnOrder`, `UnitsInStock`) stoğun siparişteki miktardan az olduğunu almak için bir sorgu yazın.
```sql
SELECT product_name, units_on_order, units_in_stock
FROM products
WHERE units_on_order < units_in_stock;
```

7. İsmi `a` ile başlayan ürünleri listeleyeniz.
```sql
SELECT *
FROM products
WHERE product_name LIKE 'a%';
```

8. İsmi `i` ile biten ürünleri listeleyeniz.
```sql
SELECT *
FROM products
WHERE product_name LIKE '%i';
```

9. Ürün birim fiyatlarına %18’lik KDV ekleyerek listesini almak (ProductName, UnitPrice, UnitPriceKDV) için bir sorgu yazın.
```sql
SELECT product_name, unit_price*18/100 + unit_price as KDV
FROM products;
```

10. Fiyatı 30 dan büyük kaç ürün var?
```sql
SELECT COUNT(*)
FROM products
WHERE unit_price > 30;
```

11. Ürünlerin adını tamamen küçültüp fiyat sırasına göre tersten listele
```sql
SELECT LOWER(product_name) AS product_name
FROM products
ORDER BY unit_price DESC;
```

12 Çalışanların ad ve soyadlarını yanyana gelecek şekilde yazdır
```sql
SELECT CONCAT(last_name, ' ', first_name) AS fullnames
FROM employees;
```

13 Region alanı NULL olan kaç tedarikçim var?
```sql
SELECT COUNT(*)
FROM suppliers
WHERE region IS NULL;
```

14. a.Null olmayanlar?

```sql
SELECT COUNT(*)
FROM suppliers
WHERE region IS NOT NULL;
```

15. Ürün adlarının hepsinin soluna TR koy ve büyültüp olarak ekrana yazdır.
```sql
SELECT UPPER(CONCAT('TR', product_name))
FROM products;
```

16. a.Fiyatı 20den küçük ürünlerin adının başına TR ekle
```sql
SELECT UPPER(CONCAT(product_name)), unit_price
FROM products
WHERE unit_price < 20;
```

17. En pahalı ürün listesini (`ProductName` , `UnitPrice`) almak için bir sorgu yazın.
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price DESC
LIMIT 1;
```

18. En pahalı on ürünün Ürün listesini (`ProductName` , `UnitPrice`) almak için bir sorgu yazın.
```sql
SELECT product_name, unit_price
FROM products
ORDER BY unit_price DESC
LIMIT 10;
```

19. Ürünlerin ortalama fiyatının üzerindeki Ürün listesini (`ProductName` , `UnitPrice`) almak için bir sorgu yazın.
```sql
SELECT product_name, unit_price
FROM products
WHERE unit_price > (SELECT AVG(unit_price) FROM products);
```

20. Stokta olan ürünler satıldığında elde edilen miktar ne kadardır.
```sql
SELECT SUM(units_in_stock * unit_price) AS total
FROM products;
```

21. Mevcut ve Durdurulan ürünlerin sayılarını almak için bir sorgu yazın.
```sql
SELECT COUNT(*)
FROM products;
```

22. Ürünleri kategori isimleriyle birlikte almak için bir sorgu yazın.
```sql
SELECT p.product_name, p.unit_price, 
       (SELECT category_name FROM Categories WHERE category_id = p.category_id) AS category_name
FROM Products p;
```

23. Ürünlerin kategorilerine göre fiyat ortalamasını almak için bir sorgu yazın.
```sql
SELECT c.category_name, AVG(p.unit_price) AS AveragePrice
FROM products p
JOIN categories c ON p.category_id = c.category_id
GROUP BY c.category_name
```

24. En pahalı ürünümün adı, fiyatı ve kategorisin adı nedir?
```sql
SELECT p.product_name, p.unit_price, c.category_name
FROM Products p
JOIN categories c ON p.category_id = c.category_id
order by p.unit_price desc limit(1)
```

25. En çok satılan ürününün adı, kategorisinin adı ve tedarikçisinin adı
```sql
SELECT p.product_name, c.category_name, s.company_name
FROM products p
JOIN categories c ON p.category_id = c.category_id
JOIN suppliers s ON p.supplier_id = s.supplier_id
ORDER BY p.units_on_order DESC
LIMIT 1;
```
