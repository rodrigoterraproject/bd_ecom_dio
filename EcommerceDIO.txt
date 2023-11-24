-- criação do banco de dados para o cenário de E-commerce

create database ecommerceDIO;
use ecommerceDIO;

-- criar tabela cliente

create table client (
		idClient int auto_increment primary key,
        Fname varchar  (10),
        Minit char (3),
        Lname varchar (20),
        CPF char (11) not null,
        Address varchar (30),
        constraint unique_cpf_client unique (CPF)
);
DESC CLIENT;
DROP TABLE CLIENT;
-- criar tabela produto

-- size dimensão do produto
drop table PRODUCT;
create table product (
		idProduct int auto_increment primary key,
        Pname varchar (10) not null,
        classification_kids bool default false, 
        category enum ('Eletrônico', 'Vestimenta', 'Brinquedos', 'Alimentos', 'Móveis') not null,
        avaliação float default 0,
        size varchar (10)
);

select * from product where Pname;
 DESC PRODUCT;
-- criar tabela pedido
desc orders;
create table orders (
		idOrder int auto_increment primary key,
        idOrderClient int,
        orderStatus enum ('Cancelado','Confirmado', 'Em processamento') not null,
        orderDescription varchar (255),
		sendValue float default 10,
        paymentCash bool default false,
        constraint fk_orders_client foreign key (idOrderClient) references client (idClient)
);

select * from orders where orderStatus;
-- para ser contuado no desafio : termine de implementar a tablea e cria a conexão com as tabelas necessárias 
-- além disso, reflita essa modificação no diagrama de esquema relacional
-- criar constraints relacionadas ao pagamento
DROP TABLE PAYMENTS;
create table payments (
		idclient int,
        idPayment int,
        typePayment enum ('Boleto', 'Cartão', 'Dois cartões'),
        limmitAvailable float,
        primary key (idClient, idpayment)
);

Select * from payments where typePayment;

desc payments;

create table inventory (
	IdInventory int auto_increment primary key,
    InventoryLocal varchar(255),
    Amount int default 0
);

drop table inventory;
desc inventory;

create table supplier (
    idSupplier int auto_increment primary key,
    SocialName varchar (255) not null,
    CNPJ char (15) not null,
    Contact char (11) not null,
    constraint unique_supplier unique (CNPJ)
);

desc supplier;

drop table productSupplier;
CREATE TABLE productSupplier (
    idProductSupplier int,
    idProductSupplierProduct int,
    Quantity int not null, 
    primary key (idProductSupplier , idProductSupplierProduct),
    constraint fk_product_supplier_supplier foreign key (idProductSupplier) references supplier (idSupplier),
    constraint fk_product_supplier_product foreign key (idProductSupplierProduct)  references product (idProduct)
);


create table Seller (
    idSeller int auto_increment primary key,
    SocialName varchar (255) not null,
    AbstName varchar(255),
    CNPJ char(15),
    Location varchar (255),
    Telephone char (11) not null,
    constraint unique_cnpj_seller unique (CNPJ)
);

drop table seller;

drop table productseller;


create table productSeller (
    idProductSeller int,
    idProduct int,
    ProductAmount int,
    primary key (idProductSeller , idProduct),
    constraint fk_product_seller foreign key (idProductSeller) references Seller (idSeller),
    constraint fk_product_product foreign key (idProduct) references Product (idProduct)
);

desc productSeller;


