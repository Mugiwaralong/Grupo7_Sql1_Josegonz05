# SOCIAL OPLESK
### 🏴‍☠️ HACKS 

<br/>

📚 tutoriales de python [tutorial 1](https://www.w3schools.com/postgresql/index.php) | [tutorial 2](https://www.tutorialesprogramacionya.com/postgresqlya/)
---

```diff
- NOTA HACER LAS PRÁCTICAS MEDIANTE coderpad.io / onecompiler.com / sqliteonline.com
```

<br/>

|Hacks | Details | 
|----------|---------|
| H-1      | REGISTER DATABASE |
| H-2      | CRUD - REGISTER DATABASE |
| H-3      | CONTACT DATABASE |
| H-4      | CRUD - CONTACT DATABASE | 
| H-5      | ECOMMERCE DATABASE |
| H-6      | CRUD |
<br/>


## 🏆 H-1
![](https://github.com/SocialOplesk/hack_sql_1/blob/main/assets/register_database.png)

![](https://github.com/SocialOplesk/hack_sql_1/blob/main/gifs/hack_sql_1_run_gif.gif)
```sh

design register database

tables:
- table countries
- table users

-----------------
⚡ example script

create table countries(
  id_country serial primary key,
  name varchar(50) not null  
);

create table users(
 id_users serial primary key,
 id_country integer not null,
 email varchar(100) not null,
 name varchar (50) not null,
 foreign key (id_country) references countries (id_country)   
);
```


## 🏆 H-2
![](https://github.com/SocialOplesk/hack_sql_1/blob/main/gifs/hack_sql_1_install_gif.gif)

```sh
crud register database

-----------------
⚡ example script

✔ create:
- insert into countries (name) values ('argentina') , ('colombia'),('chile');
- select * from countries;

- insert into users (id_country, email, name) 
  values (2, 'foo@foo.com', 'fooziman'), (3, 'bar@bar.com', 'barziman'); 
- select * from users;

✔ delete:
- delete from users where email = 'bar@bar.com';

✔ update:
- update users set email = 'foo@foo.foo', name = 'fooz' where id_users = 1;
- select * from users;

✔select:
- select * from users inner join  countries on users.id_country = countries.id_country;

- select u.id_users as id, u.email, u.name as fullname, c.name 
  from users u inner join  countries c on u.id_country = c.id_country;
```


## 🏆 H-3
![](https://github.com/SocialOplesk/hack_sql_1/blob/main/assets/contact_database.png)
```sh
design contact database

tables:
- table countries
- table priorities
- table contact_request

  create table priorities(
  id_priority serial primary key,
  type_name varchar(50) not null  
);

create table contact_request(
 id_email serial primary key,
 id_country integer not null,
 id_priority integer not null,
 name varchar(100) not null,
 detail varchar (50) not null,
 physical_address varchar (50) not null,
  
 foreign key (id_country) references countries (id_country),   
 foreign key (id_priority) references priorities (id_priority)
);



```


## 🏆 H-4
```sh
crud contact database

✔insert:
- insert 5 record in countries
- insert 3 record in priorities
- insert 3 record in contact_request

✔delete;
- delete last user:

✔update:
- update first user:

insert into  contact_request (id_country,id_priority,name,detail,physical_address) 
values (1,1,'jose','casa','calle 13'),
	   (2,2,'alberto','edificio','calle 55'),
       (3,3,'hanson','Quinta','calle 80');
       
✔ delete:
DELETE FROM contact_request
WHERE id_email = (SELECT id_email FROM contact_request ORDER BY id_email DESC LIMIT 1);

✔ UPDATE

UPDATE contact_request
SET name = 'seimus'
WHERE id_email = (SELECT id_email FROM contact_request ORDER BY id_email ASC LIMIT 1);
       
       



```


## 🏆 H-5
![](https://github.com/SocialOplesk/hack_sql_1/blob/main/assets/ecommerce_database.png)
```sh
design ecommerce database

tables:
- table countries
- table roles
- table taxes
- table offers
- table discounts
- table payments
- table customers
- table invoice_status
- table products
- table product_customers
- table invoices
- table orders

create table discounts(
id_discount serial primary key,
status BOOLEAN,
percentage NUMERIC (16,4)
  
);

create offers(
id_offer  integer not null,
status BOOLEAN
);

create taxes(
  id_tax serial primary key,
  percentage NUMERIC (16,4)

);


create table products(
 id_product serial primary key,
 id_discount integer not null,
 id_offer integer not null,
 id_tax integer not null,  
 name varchar(100) not null,
 details varchar (50) not null,
 minimum_stock varchar (50) not null,
 maximum_stock varchar (50) not null,
 current_stock varchar (50) not null,
 price NUMERIC (16,4) NOT NULL,
 price_with_tax NUMERIC (16,4) NOT NULL,
 
foreign key (id_discount) references discounts (id_discount),
foreign key (id_offer) references offers (id_offer),
foreign key (id_tax) references taxes (id_tax)
  
);

create table roles(

  id_role serial primary key,
  name varchar(100) not null
);


create table countries(

  id_country serial primary key,
  name varchar(100) not null
);

create table customers (
  id_customer serial primary key,
  email varchar(100) not null,
  id_country integer not null,
  id_role integer not null,
  name varchar(100) not null,
  age integer not null,
  password varchar(10) not null,
  physical_address varchar(100) not null,
  
foreign key (id_country) references countries (id_country),
foreign key ( id_role) references roles ( id_role)
  
);

create table products_customers(
  id_product integer not null,
  id_customer integer not null,
  
foreign key (id_product) references products (id_product),
foreign key ( id_customer) references customers (id_customer)
  

);

create table playments(
  id_payment serial primary key,
  type varchar(100) not null

);



create table invoice_status(

  id_invoice_status serial primary key,
  status varchar(100) not null
);

create table orders(

  id_order serial primary key,
  id_invoice integer not null,
  id_product integer not null,
  detail varchar(100) not null,
  amount NUMERIC (16,4) NOT NULL,
  price NUMERIC (16,4) NOT NULL,
  
foreign key (id_invoice) references invoice (id_invoice),  
foreign key (id_product) references products (id_product)
  
  
);


create  table invoice (
  id_invoice serial primary key,
  id_customer integer not null,
  id_payment integer not null,
  id_invoice_status integer not null,
  date TIMESTAMP,
  total_to_pay NUMERIC (16,4) NOT NULL,
  
foreign key (id_customer) references customers (id_customer),  
foreign key (id_payment) references payments (id_payment),
foreign key (id_invoice_status) references invoice_status (id_invoice_status) 

);
```


## 🏆 H-6
```sh
crud ecommerce database

✔insert:
- insert 3 record in all tables
- create 3 invoices

✔delete:
- delete last first user:

✔update:
- update last user:
- update all taxes:
- update all prices

insert into discounts (status,percentage) 
  values (true,10 ),
  		 (true,20 ),
         (false,30);

select * from discounts;

insert into offers (status) 
  values (true),
  		 (true),
         (false);

select * from offers;

insert into taxes (percentage) 
  values (10),
  		 (20),
         (30);

select * from taxes;



insert into products (id_discount,id_offer, id_tax, "name",details,minimum_stock,maximum_stock,current_stock,price,price_with_tax) 
  values (1,1, 1, 'resident evil','juego terror',50,100,9999,65,70),
  		 (2,2, 2, 'silent hill','juego terror',100,200,9999,70,80),
         (3,3, 3, 'alone the dark','juego terror',300,400,9999,80,90);
select * from products;


insert into roles (name) 
  values ('usuario'),
  		 ('supervisor'),
         ('administrador');

select * from roles;


insert into countries (name) 
  values ('venezuela'),
  		 ('argentina'),
         ('peru');

select * from countries;

insert into customers (email,id_country,id_role,name,age,password,physical_address) 
  values ('jose@usuario.com',1,1,'jose',40,123456,'caracas'),
  		 ('alberto@usuario.com',1,1,'alberto',40,123456,'valencia'),
         ('long@usuario.com',1,1,'long',40,123456,'maracay');

select * from customers;


insert into products_customers (id_product,id_customer) 
  values (5,1),
  		 (6,2),
         (7,3);
         
select * from products_customers;


insert into payments (type) 
  values ('efectivo'),
  		 ('transferencia'),
         ('deposito');
         
select * from payments;


insert into invoice_status (status) 
  values ('activo'),
  		 ('En proceso'),
         ('inactivo');
         
select * from invoice_status;



insert into invoice (id_customer,id_payment,id_invoice_status,date,total_to_pay) 
  values (1,1,1,'05-24-2024',100),
  		 (2,2,2,'06-24-2024',200),
         (3,3,3,'07-24-2024',300);
         
select * from invoice;

insert into orders (id_invoice,id_product,detail,amount,price) 
  values (1,5,'Pedido0',100,60),
  		 (1,6,'Pedido1',200,70),
         (1,7,'Pedido2',300,80);
         
select * from invoice;         
select * from orders;


--✔delete:
-- delete last first user:

delete from roles where name = 'administrador';

--✔update:
-- update last user:
-- update all taxes:
-- update all prices

update roles set name = 'manager' where id_role=2;
select * from roles;


update taxes set percentage = 15 where id_tax=1;
update taxes set percentage = 20 where id_tax=2;
update taxes set percentage = 25 where id_tax=3;

select * from taxes;


update products set price = 80 where id_product=5;
update products set price = 90 where id_product=6;
update products set price = 100 where id_product=7;
select  * from products;


select * from countries;
select * from roles;
select * from taxes;
select * from offers;
select * from discounts;
select * from payments;
select * from customers;
select * from invoice_status;
select * from products;
select * from product_customers;
select * from invoices;
select * from orders;


alter table invoice rename to invoices;
);
```
