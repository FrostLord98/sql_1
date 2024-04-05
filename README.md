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
