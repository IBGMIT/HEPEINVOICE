
                                                              Peders hjemmemekka LESMEGFIL
1. Last ned Xampp - og følg de jævla instruksjonene på hjemmesiden. Xampp er det spennende programmet som skal hoste webserveren for vår under utviklingsfasen. Xampp skal lagres på C:\
2. Deretter tar du å kloner/laster ned denne bitchen, det skal legges i følgende folder: C:\xamppp\htdocs\
3. Åpne deretter MYSQL og opprett et schema som heter "banks": kjør så de forskjellige koder som jeg har lagt ved under.
4. Gå deretter inn i Invoice.php filen på hepeconsulting, og endre parametrene for SQL.
5. Nå åpner du så XAMPP Control Panel og trykker start på apache. Deretter åpner du linken: http://localhost/hepeconsulting/invoice_list.php
6. Deretter koder du i vei og vippser 500kr til 40540148.






SQL:

CREATE TABLE `invoice_user` (
`id` int(11) NOT NULL,
`email` varchar(100) NOT NULL,
`password` varchar(100) NOT NULL,
`first_name` varchar(100) NOT NULL,
`last_name` varchar(100) NOT NULL,
`mobile` bigint(20) NOT NULL,
`address` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


CREATE TABLE `invoice_order` (
`order_id` int(11) NOT NULL,
`user_id` int(11) NOT NULL,
`order_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
`order_receiver_name` varchar(250) NOT NULL,
`order_receiver_address` text NOT NULL,
`order_total_before_tax` decimal(10,2) NOT NULL,
`order_total_tax` decimal(10,2) NOT NULL,
`order_tax_per` varchar(250) NOT NULL,
`order_total_after_tax` double(10,2) NOT NULL,
`order_amount_paid` decimal(10,2) NOT NULL,
`order_total_amount_due` decimal(10,2) NOT NULL,
`note` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


CREATE TABLE `invoice_order_item` (
`order_item_id` int(11) NOT NULL,
`order_id` int(11) NOT NULL,
`item_code` varchar(250) NOT NULL,
`item_name` varchar(250) NOT NULL,
`order_item_quantity` decimal(10,2) NOT NULL,
`order_item_price` decimal(10,2) NOT NULL,
`order_item_final_amount` decimal(10,2) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


CREATE TABLE `customer` (
`customer_id` int(11) not null auto_increment,
`company_name` varchar(250) NOT NULL,
`email` varchar(250) NOT NULL,
`street_address` varchar(250) NOT NULL,
`postal_code` int(11) NOT NULL,
`city` varchar(250) NOT NULL,
`telephone_number` int(11) NOT NULL,
`organizational_number` int(11) NOT NULL,
`reference` varchar(250) NOT NULL,
primary key (`customer_id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

CREATE TABLE `timetable` (
  `project_id` int(11) NOT NULL AUTO_INCREMENT,
  `date` date NOT NULL,
  `time_defintion` varchar(250) NOT NULL,
  `description` varchar(250) NOT NULL,
  `time` int(11) NOT NULL,
  PRIMARY KEY (`project_id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=latin1

drop table if exists `project`;
CREATE TABLE `project` (
`project_id` int(11) not null auto_increment,
`date_created` timestamp NOT NULL,
`customer_id` int(11) NOT NULL,
`sats` int(11) NOT NULL,
primary key (`project_id`),
foreign key (`customer_id`) references banks.customer (`customer_id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;



INSERT STATEMENTS A LA PEDER:
insert into banks.invoice_order (user_id,order_receiver_name, order_receiver_address, order_total_before_tax, order_total_tax,order_tax_per,order_total_after_tax,order_amount_paid,order_total_amount_due,note) values (1,"Confirmit","Karenlyst Alle",1000.00,200.00,"20%",1200.00,0,1200.00,"hei");
insert into banks.invoice_order_item (order_id,item_code,item_name,order_item_quantity,order_item_price,order_item_final_amount) values (1,"1","Konsulenttimer etter godkjent timeliste",30.00,3000.00,90.000);
insert into project (customer_id,sats) values (1,3000);
insert into customer (company_name,email,street_address, postal_code,city,telephone_number,organizational_number,reference) values ('Confirmit',"confirmit@confirmit.com","Karenlyst alle 53",0279,"Oslo",21502500,976886240,"Ken Østereng");
Insert into timetable (date,time_defintion,description,time) values ('2020-03-17',"days","Litta sidejobb på si da",30)
