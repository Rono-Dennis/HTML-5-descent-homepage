 create table users(
     user_id int(10) auto_increment not null primary key,
     username varchar(50) not null,
     password varchar(64) not null,
     category varchar(50) not null,
     register_date timestamp default current_timestamp on update current_timestamp,
     gender varchar(20) not null,
     name varchar(20) not null,
     phone varchar(20) not null
     );
	 
create table organizations(
organization_id int(10) not null primary key,
organization_name varchar(50) not null,
organization_description VARCHAR(255) not null
);

/*
users and oganizations have one to many relationships. This can be solved as shown below using foreign keys
*/
ALTER TABLE users
ADD organization_id varchar(10);

ALTER TABLE users
ADD FOREIGN KEY (organization_id) REFERENCES organizations(organization_id);


/*
users and meetins/events have many to many relationships. This can be solved as shown below using foreign keys
*/
create table meetings(
meeting_id int(10) auto_increment not null PRIMARY key,
meeting_description VARCHAR(50) not null unique,
meeting_start_time date not null,
meeting_end_time date not null,
meeting_type VARCHAR(50) not null
);

/*
create a common table for users and meetings to handle many to many relationships*/
/*use primary key fields from participating entities exactly the way they are*/
create table usersmeetings(
user_id int(10) not null unique,
meeting_id int(10) not null unique,
foreign key(user_id) REFERENCES users(user_id),
FOREIGN KEY(meeting_id)REFERENCES meetings(meeting_id)
);

/*view th database schema*/
select 
table_schema,
table_name,
column_name,
constraint_name
from 
information_schema.key_column-usage
where 
referenced_table_schema is not null;