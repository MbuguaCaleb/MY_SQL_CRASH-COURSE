```
CREATE DATABASE record_company;

USE record_company;

CREATE TABLE bands(
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  PRIMARY KEY (id) 
);

##References is important because we cannot add an id that's not existent
##Whe we delete  a band its as well going to throw an error that there are
##Exisiting bands with the same ID.

CREATE TABLE albums(
id INT NOT NULL AUTO_INCREMENT,
name VARCHAR(255) NOT NULL,
release_year INT,
band_id INT NOT NULL,
PRIMARY KEY (id),
FOREIGN KEY(band_id) REFERENCES bands(id)
);


#Single Insert
INSERT INTO bands(name) 
VALUES ('KAG Naivasha');

#Multiple Inserts
INSERT INTO bands (name)
VALUES ('JKUAT CU'),('MURANGA CU'),('DEDAN KIMATHI CU');

##FETCH DATA

SELECT * FROM bands;

##LIMIT
SELECT * FROM bands LIMIT 2;

##SELECT SPECIFIED COLUMNS
SELECT name FROM bands;

##Rename columns ALIAS
SELECT id AS 'ID', name AS 'Band Name'
FROM bands;

#lastest to the first
SELECT * FROM bands
ORDER BY name;

SELECT * FROM bands
ORDER BY name DESC;


INSERT INTO albums (name,release_year,band_id)
VALUES ('The Promise',1985,1),
       ('MY WORSHIP',2021,1),
       ('AFLEWO',2021,2),
       ('ACOUSTIC',NULL,3),
       ('UNASHAMED PRAISE',2019,4),
	   ('UNASHAMED PRAISE TWO',2020,5);
       
SELECT * FROM albums;


SELECT DISTINCT name FROM albums;

UPDATE albums
SET release_year = 1982
WHERE id=1;

SELECT * FROM albums
WHERE release_year < 2000;

SELECT * FROM albums
WHERE name LIKE '%ne%';

SELECT * FROM albums
WHERE name LIKE '%ne%' OR band_id =2 ;


SELECT * FROM albums
WHERE release_year = 1985 AND band_id =1;

SELECT * FROM albums
WHERE release_year BETWEEN 2000 AND 2022;

SELECT * FROM albums
WHERE release_year IS NULL;

DELETE FROM albums
WHERE id = 5;

SELECT * FROM albums;

#INNER JOIN
#Only returns values that have a match between
#the left and the right table
SELECT * FROM bands 
JOIN albums ON bands.id = albums.band_id;

#LEFT JOIN
#Lists everything from the left side even 
#if they do not have a march

#Will return all bands even if they do not have an album
SELECT * FROM bands 
LEFT JOIN albums ON bands.id = albums.band_id;

#Will return everything from the table on the right
#If there is an albumn with no table associated

#RIGHT JOIN
SELECT * FROM bands 
RIGHT JOIN albums ON bands.id = albums.band_id;

SELECT * FROM albums
RIGHT JOIN bands ON bands.id = albums.band_id;


##aggregate functions and grouping BY

SELECT AVG(release_year) FROM albums;

SELECT SUM(release_year) FROM albums;

SELECT band_id,COUNT(band_id) FROM albums

GROUP BY band_id;

##Aggregate data is queried using a 
##Having after group by
SELECT b.name AS band_name, COUNT(a.id) 
as num_albums
FROM bands b
LEFT JOIN albums a ON b.id=a.band_id
GROUP BY b.id
HAVING num_albums=1;

##Where statements happen before the group by
##Good to Note
 



```