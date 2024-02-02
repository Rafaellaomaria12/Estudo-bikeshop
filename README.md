# Estudo caso
## Caso bike shop

### Empresa: BikeShop

### Visão Geral:
A BikeShop é uma empresa especializada na venda de bicicletas e acessórios relacionados. 
Localizada em uma área urbana movimentada de Uberlândia, Minas Gerais, a empresa tem 
como objetivo oferecer uma variedade de bicicletas de alta qualidade para ciclistas de todos os 
níveis, desde iniciantes até ciclistas experientes e entusiastas.

### Desafio:
A BikeShop está crescendo rapidamente e enfrenta desafios no gerenciamento eficiente de seu 
inventário, clientes e vendas. Atualmente, eles estão registrando essas informações 
manualmente ou usando planilhas eletrônicas, o que se tornou ineficiente e propenso a erros. 
Eles reconhecem a necessidade de um sistema de banco de dados centralizado que possa 
armazenar e gerenciar essas informações de forma mais eficaz.

### Objetivos do Sistema de Banco de Dados:
Gerenciar o inventário de bicicletas e acessórios, incluindo detalhes como modelo, marca, 
quantidade em estoque, preço de venda e fornecedor.
Manter um registro centralizado de clientes, incluindo informações como nome, endereço, 
número de telefone, endereço de e-mail e histórico de compras.
Registrar e acompanhar as vendas de bicicletas e acessórios, incluindo detalhes como data da 
venda, produtos vendidos, preço de venda, método de pagamento e vendedor responsável.

Requisitos Funcionais do Sistema de Banco de Dados:
Capacidade de adicionar, atualizar e excluir itens do inventário, bem como verificar a 
disponibilidade de produtos em tempo real.

Capacidade de adicionar novos clientes, atualizar informações existentes e manter um histórico 
de suas compras anteriores.
Funcionalidade para registrar novas vendas, incluindo a associação dos produtos vendidos aos 
clientes correspondentes e a geração de recibos.
Recursos de segurança para proteger os dados do cliente e do inventário contra acesso não 
autorizado.
Capacidade de gerar relatórios de vendas, análises de estoque e dados do cliente para ajudar 
na tomada de decisões comerciais.

### Abordagem Proposta:
A BikeShop planeja desenvolver um sistema de banco de dados personalizado usando 
tecnologias modernas de banco de dados, como MySQL ou PostgreSQL. Eles planejam 
colaborar com desenvolvedores de software especializados para projetar e implementar o 
sistema de acordo com seus requisitos específicos. O sistema será acessado por funcionários 
autorizados por meio de uma interface de usuário intuitiva, onde poderão realizar todas as 
operações necessárias de forma eficiente.

Benefícios Esperados:
Melhoria na eficiência operacional, permitindo que a BikeShop gerencie seu inventário, clientes 
e vendas de forma mais rápida e precisa.
Maior satisfação do cliente, oferecendo um serviço mais personalizado e mantendo um 
histórico detalhado das interações anteriores.
Melhoria na tomada de decisões comerciais com base em relatórios e análises de dados 
precisos e atualizados.

Com um sistema de banco de dados eficiente e bem projetado, a BikeShop está confiante de 
que poderá atender às demandas de seus clientes de maneira mais eficaz e continuar 
prosperando no mercado de bicicletas.
Modelo lógico para o estudo de caso

Tabelas:





### Relacionamentos:
Um fornecedor pode fornecer múltiplos itens de inventário, mas cada item de inventário é 
fornecido por apenas um fornecedor. 
(Relacionamento um para muitos entre Fornecedores e 
Inventário)

Um cliente pode fazer várias compras, mas cada compra é feita por apenas um cliente. 
(Relacionamento um para muitos entre Clientes e Vendas)

Cada venda inclui vários itens de inventário, e cada item de inventário pode estar presente em 
várias vendas. 
(Relacionamento muitos para muitos entre Vendas e Inventário)

Um vendedor pode fazer várias vendas, mas cada venda é realizada por apenas um vendedor. 
(Relacionamento um para muitos entre Vendedores e Vendas)

Cada vendedor é associado a apenas um funcionário. 
(Relacionamento um para um entre Funcionários e Vendedores)

Este modelo lógico de banco de dados reflete as entidades principais e seus relacionamentos 
no contexto da BikeShop, permitindo a organização eficiente dos dados e a realização de 
operações de negócios necessária.


### Com base no estudo de base acima, foi construido um modelo conceitual para desenvolvimento de um banco de dados que atenda a Bike Shope.

# Modelo Conceitual
![](bikeshop2.png)

# Modelo Lógico
![](bikeshop.png)

### Código SQL para modelo físico de banco de dados

``` -- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`fornecedor`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`fornecedor` (
  `idfornecedor` INT NOT NULL AUTO_INCREMENT,
  `nomeforcedor` VARCHAR(40) NOT NULL,
  `enderecofornecedor` VARCHAR(30) NOT NULL,
  `telefonefornecedor` VARCHAR(15) NOT NULL,
  `emailfornecedor` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`idfornecedor`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Inventario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Inventario` (
  `idinventario` INT NOT NULL AUTO_INCREMENT,
  `modelo` VARCHAR(30) NOT NULL,
  `marca` VARCHAR(30) NOT NULL,
  `quantidade` INT NOT NULL,
  `Preco` DECIMAL NOT NULL,
  `fornecedor_idfornecedor` INT NOT NULL,
  PRIMARY KEY (`idinventario`, `fornecedor_idfornecedor`),
  INDEX `fk_Inventario_fornecedor1_idx` (`fornecedor_idfornecedor` ASC) VISIBLE,
  CONSTRAINT `fk_Inventario_fornecedor1`
    FOREIGN KEY (`fornecedor_idfornecedor`)
    REFERENCES `mydb`.`fornecedor` (`idfornecedor`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Vendedores`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Vendedores` (
  `idvendedores` INT NOT NULL AUTO_INCREMENT,
  `nomevendedores` VARCHAR(35) NULL,
  `Venda_idVenda` INT NOT NULL,
  PRIMARY KEY (`idvendedores`, `Venda_idVenda`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Venda`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Venda` (
  `idVenda` INT NOT NULL AUTO_INCREMENT,
  `valor` DECIMAL(10,2) NOT NULL,
  `data` DATE NOT NULL,
  `quantidade` INT NOT NULL,
  `precototal` DECIMAL(10,2) NOT NULL,
  `metododepagamento` VARCHAR(45) NOT NULL,
  `Vendedores_idvendedores` INT NOT NULL,
  `Vendedores_Venda_idVenda` INT NOT NULL,
  PRIMARY KEY (`idVenda`, `Vendedores_idvendedores`, `Vendedores_Venda_idVenda`),
  INDEX `fk_Venda_Vendedores1_idx` (`Vendedores_idvendedores` ASC, `Vendedores_Venda_idVenda` ASC) VISIBLE,
  CONSTRAINT `fk_Venda_Vendedores1`
    FOREIGN KEY (`Vendedores_idvendedores` , `Vendedores_Venda_idVenda`)
    REFERENCES `mydb`.`Vendedores` (`idvendedores` , `Venda_idVenda`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`cliente`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`cliente` (
  `idcliente` INT NOT NULL AUTO_INCREMENT,
  `nomecliente` VARCHAR(50) NOT NULL,
  `endereco` VARCHAR(45) NOT NULL,
  `telefonecliente` VARCHAR(15) NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  `Venda_idVenda` INT NOT NULL,
  `Venda_Vendedores_idvendedores` INT NOT NULL,
  `Venda_Vendedores_Venda_idVenda` INT NOT NULL,
  PRIMARY KEY (`idcliente`, `Venda_idVenda`, `Venda_Vendedores_idvendedores`, `Venda_Vendedores_Venda_idVenda`),
  INDEX `fk_cliente_Venda1_idx` (`Venda_idVenda` ASC, `Venda_Vendedores_idvendedores` ASC, `Venda_Vendedores_Venda_idVenda` ASC) VISIBLE,
  CONSTRAINT `fk_cliente_Venda1`
    FOREIGN KEY (`Venda_idVenda` , `Venda_Vendedores_idvendedores` , `Venda_Vendedores_Venda_idVenda`)
    REFERENCES `mydb`.`Venda` (`idVenda` , `Vendedores_idvendedores` , `Vendedores_Venda_idVenda`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`funcionarios`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`funcionarios` (
  `idfuncionario` INT NOT NULL AUTO_INCREMENT,
  `cargo` VARCHAR(20) NOT NULL,
  `salario` DECIMAL(10,5) NOT NULL,
  `datadeadmissao` DATE NOT NULL,
  `Vendedores_idvendedores` INT NOT NULL,
  `Vendedores_Venda_idVenda` INT NOT NULL,
  PRIMARY KEY (`idfuncionario`, `Vendedores_idvendedores`, `Vendedores_Venda_idVenda`),
  INDEX `fk_funcionarios_Vendedores1_idx` (`Vendedores_idvendedores` ASC, `Vendedores_Venda_idVenda` ASC) VISIBLE,
  CONSTRAINT `fk_funcionarios_Vendedores1`
    FOREIGN KEY (`Vendedores_idvendedores` , `Vendedores_Venda_idVenda`)
    REFERENCES `mydb`.`Vendedores` (`idvendedores` , `Venda_idVenda`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Venda_has_Inventario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Venda_has_Inventario` (
  `Venda_idVenda` INT NOT NULL,
  `Inventario_idinventario` INT NOT NULL,
  PRIMARY KEY (`Venda_idVenda`, `Inventario_idinventario`),
  INDEX `fk_Venda_has_Inventario_Inventario1_idx` (`Inventario_idinventario` ASC) VISIBLE,
  INDEX `fk_Venda_has_Inventario_Venda1_idx` (`Venda_idVenda` ASC) VISIBLE,
  CONSTRAINT `fk_Venda_has_Inventario_Venda1`
    FOREIGN KEY (`Venda_idVenda`)
    REFERENCES `mydb`.`Venda` (`idVenda`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Venda_has_Inventario_Inventario1`
    FOREIGN KEY (`Inventario_idinventario`)
    REFERENCES `mydb`.`Inventario` (`idinventario`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;


```
