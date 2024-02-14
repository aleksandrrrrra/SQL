# SQL
FROM country
WHERE (IndepYear BETWEEN 1800 and 1899) and Continent like "Europe%";
--Страны, в названиях которых содержат слог “ра”  (9 записей)
SELECT Name
FROM country
WHERE name LIKE '%pa%';
--Страны, названия которых начинаются на гласную букву  (A, E, I, O, U, Y) (42 записи);
SELECT Name
FROM country 
WHERE name RLIKE '^[A, E, I, O, U, Y]';
--Страны, названия которых начинаются и заканчиваются на одну и ту же букву. (20 записей)
SELECT Name
FROM country
WHERE LEFT(Name, 1) = RIGHT(Name, 1);
--Государства, формой правления которых является различной формы монархия (43 записи)
SELECT Name, GovernmentForm
FROM country
WHERE GovernmentForm like '%monarchy%';
--Страны, население которых меньше 1 млн. (85 записей)
SELECT Name
FROM country
WHERE Population < 1000000;
--Самое древнее государство (China)
SELECT Name
FROM country
order by IndepYear LIMIT 1;
--Самое маленькое по площади государство (Holy See (Vatican City State))
SELECT Name, SurfaceArea
FROM country 
ORDER BY SurfaceArea LIMIT 1;
--Первую десятку наиболее населенных государств мира
SELECT Name, Population
FROM country 
ORDER BY Population DESC LIMIT 10;
--Первую десятку наиболее населенных государств Европы
SELECT Name, Population
FROM country 
WHERE Continent LIKE 'europe'
ORDER BY Population DESC LIMIT 10;
--Cуммарное число жителей стран Европы и суммарную площадь её государств (730 074 600, 23 049 133.9)
SELECT SUM(Population) AS 'Kokku elanike_arv',
SUM(SurfaceArea) AS 'Kokku pindala'
FROM country
WHERE Continent like '%europe%';
--Число стран, расположенных не в Антарктике (234 записи)
SELECT COUNT(Name)
FROM country
WHERE Continent NOT LIKE '%antarctica%';
--Число стран, где главой правительства является Елизавета II (Elisabeth II), суммарное число жителей этих стран.  (35 стран, 122 872 550 человек)
SELECT SUM(Population), COUNT(*)
FROM country
WHERE HeadOfState LIKE 'Elisabeth II';
--Число стран, наибольшее и наименьшее число жителей стран Полинезии (Polynesia) (10 стран, 235 000 человек, 50 человек)
SELECT COUNT(*) as RiikideArv, MIN(Population) as Min, MAX(Population) as Max
FROM country
WHERE Region LIKE "Polynesia";
