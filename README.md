CREATE TABLE Product(
prod_id	     CHAR(10),
pname	     VARCHAR(30),
price	     DECIMAL);

ALTER TABLE Product ADD CONSTRAINT pk_product PRIMARY KEY (prod_id);
ALTER TABLE Product ADD CONSTRAINT ck_product_price CHECK (price > 0);

INSERT INTO Product(prod_id, pname, price) VALUES
('p1', 'tape', 2.5),
 ('p2', 'tv', 250),
 ('p3', 'vcr', 80);

CREATE TABLE Depot(
dep_id	     CHAR(10),
addr	     VARCHAR(30),
volume	     INTEGER);

ALTER TABLE Depot ADD CONSTRAINT pk_depot PRIMARY KEY (dep_id);
ALTER TABLE Depot ADD CONSTRAINT ck_depot_volume CHECK (volume > 0);

INSERT INTO Depot(dep_id, addr, volume) VALUES
('d1', 'New York', 9000),
('d2', ' Syracuse ', 6000),
('d4', ' New York ',2000);

CREATE TABLE Stock(
prod_id	     CHAR(10),
dep_id	     CHAR(10),
quantity	     INTEGER);

ALTER TABLE Stock ADD CONSTRAINT pk_stock PRIMARY KEY (prod_id, dep_id);
ALTER TABLE Stock ADD CONSTRAINT fk_stock_prod FOREIGN KEY(prod_id) 
REFERENCES Product(prod_id);
ALTER TABLE Stock ADD CONSTRAINT fk_stock_dep FOREIGN KEY(dep_id) 
REFERENCES Depot(dep_id);


INSERT INTO Stock(prod_id, dep_id, quantity) VALUES
('p1', 'd1', 1000),
('p1', 'd2', -100),
('p1', 'd4', 1200),
('p3', 'd1', 3000),
('p3', 'd4', 2000),
('p2', 'd4', 1500),
('p2', 'd1', -400),
('p2', 'd2', 2000);

In pgAdmin 4, go to the database called postgres: 
Or
In SQL Shell (psql):
Show tables
\c postgres
\dt


Show all entries in the table: 
TABLE product;
TABLE depot;
TABLE stock;

#1 transaction： The product p1 is deleted from Product and Stock:

DELETE FROM stock
WHERE prod_id='p1';
DELETE FROM product
WHERE prod_id='p1';

Show all entries after deleting: 
TABLE product;
TABLE stock;
