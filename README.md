![WhatsApp Image 2024-03-31 at 3 06 57 PM](https://github.com/FrostLord98/sql_1/assets/110127391/670b4109-ed50-4242-8e66-6751713f0f5b)


create table countries(
  id_country serial primary key,
  name varchar(50) not null  
);


create table users(
  id_users serial primary key,
  id_country integer not null,
  email varchar (100) not null,
  name varchar (50) not null,
  foreign key (id_country) references countries (id_country)
);

![WhatsApp Image 2024-03-31 at 3 09 10 PM](https://github.com/FrostLord98/sql_1/assets/110127391/42aec2bb-a601-4c1b-9c8a-f33abef186aa)

create table countries(
  id_country serial primary key,
  name varchar(50) not null  
);


create table users(
  id_users serial primary key,
  id_country integer not null,
  email varchar (100) not null,
  name varchar (50) not null,
  foreign key (id_country) references countries (id_country) 
);

insert into countries (name) values ('argentina') , ('colombia'),('chile');
select * from countries;

insert into users (id_country, email, name)
values(2, 'foo@foo.com', 'fooziman'), (3, 'bar@bar.com', 'barziman');
select * from users;


 delete from users where email = 'bar@bar.com';


update users set email = 'foo@foo.foo', name = 'fooz' where id_users = 1;
select * from users;

select * from users inner join  countries on users.id_country = countries.id_country;
select u.id_users as id, u.email, u.name as fullname, c.name 
from users u inner join  countries c on u.id_country = c.id_country;

![WhatsApp Image 2024-03-31 at 4 11 54 PM](https://github.com/FrostLord98/sql_1/assets/110127391/2fdba9db-1ac1-498d-8c8c-1e30e0405113)

create table countries(
  id_country serial primary key,
  name varchar(50) not null  
);

create table priorities(
  id_priority serial primary key,
  type_name varchar(50) not null
);

create table contact_request(
  id_email varchar (50) not null,
  id_country integer not null,
  id_priority integer not null,
  name varchar (50) not null,
  detail text not null,
  physical_address text not null,
  foreign key (id_country) references countries (id_country),
  foreign key (id_priority) references priorities (id_priority)
);

![WhatsApp Image 2024-03-31 at 4 12 02 PM (1)](https://github.com/FrostLord98/sql_1/assets/110127391/3564e56f-95b3-4629-8ff7-46b96fe918d3)


create table countries(
  id_country serial primary key,
  name varchar(50) not null  
);

create table priorities(
  id_priority serial primary key,
  type_name varchar(50) not null
);

create table contact_request(
  id_email varchar (50) not null,
  id_country integer not null,
  id_priority integer not null,
  name varchar (50) not null,
  detail text not null,
  physical_address text not null,
  foreign key (id_country) references countries (id_country),
  foreign key (id_priority) references priorities (id_priority)
);

insert into countries(id_country, name)
 values (1,'venezuela'), (2,'fooland'), (3,'argentina'),(4,'chile'),(5,'ecuador');
select * from countries;

insert into priorities(id_priority,type_name)
 values (1,'high'), (2, 'mid'), (3, 'low');
select * from priorities;

insert into contact_request(id_email,id_country,id_priority,name,detail,physical_address)
 values ('foo@foo.foo',1,1,'fooziman','none', 'venezuela'), 
 ('bar@bar.bar',1,1, 'barziman','none', 'venezuela'),
 ('qux@qux.qux',1,1, 'qux','none', 'venezuela');
select * from contact_request;

delete from contact_request where name = 'qux';

select * from contact_request;

update contact_request set id_country =2,  physical_address = 'fooland' 
where name = 'fooziman';
select * from contact_request;

![WhatsApp Image 2024-04-05 at 1 48 29 PM](https://github.com/FrostLord98/sql_1/assets/110127391/b4788ed6-3d0d-4a75-b2d6-9d55677fa1c1)


create table countries(
  id_country serial primary key not null,
  name varchar(50) not null
);

create table roles (
  id_role serial primary key not null,
  name varchar(50) not null
);

create table taxes(
  id_tax serial primary key not null,
  percentage varchar(5)
);

create table offers (
  id_offer serial primary key not null,
  status varchar(20) not null
);

create table discounts (
  id_discount serial primary key not null,
  status varchar(20) not null,
  percentage varchar(5)
);

create table payments (
  id_payment serial primary key not null,
  _type varchar(20) not null
);

create table customers(
  id_customer serial primary key not null,
  id_country integer not null,
  id_role integer not null,
  email varchar(50) not null,
  name varchar(50) not null,
  age integer not null,
  password varchar(50) not null,
  physical_addresss text not null,
  foreign key (id_country) references countries (id_country),
  foreign key (id_role) references roles (id_role)
);

create table invoice_status (
  id_invoice_status serial primary key not null,
  status varchar(20) not null
);

create table products (
  id_product serial primary key not null,
  id_discount integer not null,
  id_offer integer not null,
  id_tax integer not null,
  name text not null,
  details text,
  minimum_stock integer not null,
  maximum_stock integer not null,
  current_stock integer not null,
  price integer not null,
  price_with_tax integer,
  foreign key (id_discount) references discounts (id_discount),
  foreign key (id_offer) references offers (id_offer),
  foreign key (id_tax) references taxes (id_tax)
);

create table products_customers(
  id_product integer not null,
  id_customer integer not null,
  foreign key (id_customer) references customers (id_customer),
  foreign key (id_product) references products (id_product),
  PRIMARY KEY (id_customer, id_product)
);

create table invoices(
  id_invoice serial primary key not null,
  id_customer integer not null,
  id_payment integer not null,
  id_invoice_status integer not null,
  _date date not null,
  total_to_pay integer not null,
  foreign key (id_customer) references customers (id_customer),
  foreign key (id_payment) references payments (id_payment),
  foreign key (id_invoice_status) references invoice_status (id_invoice_status)
);

create table orders (
  id_order serial primary key not null,
  id_invoice integer not null,
  id_product integer not null,
  detail text not null,
  amount integer not null,
  price integer not null,
  foreign key (id_invoice) references invoices (id_invoice),
  foreign key (id_product) references products (id_product)
);

