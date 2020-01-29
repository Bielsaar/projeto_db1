# Equipe
- Gustavo Sousa Galisa Albuquerque - mat. 20191370046
- Gabriel Xavier - mat. 20191370025
- Cláudio Cruz - mat. 20191370006

------------

# Índice

1. Minimundo
2. Modelo conceitual
3. Modelo lógico
5. Dicionário de dados
- 5.1  Tabela Funcionário
- 5.2  Tabela Secretária
- 5.3  Tabela Contador
- 5.4  Tabela Advogado
- 5.5  Tabela Consulta
- 5.6  Tabela Agenda
- 5.7  Tabela Cliente
- 5.8  Tabela Física
- 5.9  Tabela Jurídica
- 5.10 Tabela Telefone
- 5.11 Tabela Gera
- 5.12 Tabela Contrato
- 5.13 Tabela Processo
- 5.14 Tabela Vinculado
- 5.15 Tabela Defensor
- 5.16 Tabela Réu
- 5.17 Tabela Testemunha
- 5.18 Tabela Juiz
- 5.19 Tabela Vara
6. Script de Criação do BD
7. Script de povoamento do BD
8. Scripts de alterações

------------
# 1. Minimundo de um escritório de advocacia

Um escritório de advocacia tem três tipos de funcionários: secretária, que também faz a organização dos arquivos e precisa ter conhecimentos de arquivologia, contadores, para realizar perícias contábeis em processos de auditoria, e uma equipe de advogados, que atuam nas áreas civil, trabalhista e administrativa/tributária e são chefiados por um advogado;

Os funcionários possuem um nome, uma matrícula, um email e um telefone profissional. Além disso, a secretária possui registro no Conselho Federal de Arquivologia, enquanto o contador obrigatoriamente é registrado junto ao Conselho de Contabilidade e os advogados possuem OAB própria;

O público alvo desse escritório são pessoas jurídicas (empresas e municípios), mas ele também pode atender a pessoas físicas em demandas específicas;

Os clientes são registrados com nome, CPF ou CNPJ, logradouro completo e telefone (s), que podem ser fixos ou celulares;

Inicialmente, é agendada, com data e hora previamente estabelecida, uma consultoria entre o cliente e um advogado. Caso haja necessidade, o contador poderá auxiliar na elaboração do processo judicial ou parecer;

Durante a consultoria, através de uma pauta específica para cada consulta, será verificada a complexidade do caso e, a partir disso, um contrato é assinado, com um identificador, e um número próprio;

Após a consultoria, poderá ou não surgir um processo. Se surgir, esse processo será de responsabilidade de um ou mais advogados e conterá obrigatoriamente o número do contrato que o fez surgir, um número identificador único gerado pelo sistema da justiça e um número identificador.O processo também estará vinculado a um réu, ao seu defensor e testemunha, além da vara e juiz responsável pela causa ;

O réu é registrado com nome, logradouro completo, telefone e email;

Por sua vez, o réu também possui um advogado constituído (defensor), com nome e OAB, ou é defendido pela defensoria pública;

A testemunha, que possui um id, nome, telefone e email também está ligada ao réu e ao defensor, formando o polo passivo que irá compor o processo;

O processo ainda está vinculado a uma vara, que conterá endereço e número especificador;

Toda vara está diretamente ligada e é coordenada por apenas um juiz de direito, que possui nome e matrícula.

------------

# 2. Modelo conceitual
![](https://github.com/gustavogalisa/projeto_db1/blob/master/projeto_revisado/Conceitual_1_FINAL_revisado_img.png)

------------

# 3. Modelo lógico
![](https://github.com/gustavogalisa/projeto_db1/blob/master/projeto_revisado/Modelo%20Logico%20Completo%20e%20Corrigido%2C%20em%20PNG.png)


------------

# 5. Dicionário de dados


**5.1 Tabela Funcionário**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  INT | NÃO  | X  |   | |
| nome  | VARCHAR(45)  | NÃO  |   |   | X|
| telefone  |BIGINT  | NÃO  |   |   | |
| email  | VARCHAR(45)  | NÃO  |   |   | | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  Chave primária | Identificador do funcionário  | PK_funcionario  | PRIMARY KEY (idfuncionario) |
| nome  | Chave alternativa  | Nome do funcionário  | AK_funcionario  | UNIQUE (nome) | |

**5.2 Tabela Secretária**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  INT | NÃO  | x  | x  | |
| cfa  | INT  | NÃO  |   |   | x| |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  Chave primária | Identificador do funcionário | PK_secretaria | PRIMARY KEY (idfuncionario, cfa)  |
|  idfuncionario | Chave estrangeira | Chave estrangeira referenciando coluna idfuncionario da tabela funcionario | FK_scretaria_funcionario  |  FOREIGN KEY (idfuncionario) REFERENCES funcionario |
|  cfa |  Chave candidata  | Indica o registro no Conselho Federal de Arquivologia  | AK_secretaria  | UNIQUE (cfa) |

**5.3 Tabela Contador**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  INT | NÃO  | x  | x  | |
| crc  | INT  | NÃO  |   |   | x | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  Chave primária | Identificador do funcionario | PK_contador | PRIMARY KEY (idfuncionario, crc)  |
|  idfuncionario | Chave estrangeira |  Chave estrangeira referenciando coluna idfuncionario da tabela funcionario | FK_contador_funcionario  |  FOREIGN KEY (idfuncionario) REFERENCES funcionario |
|  crc |  Chave candidata  | Indica o registro no Conselho Regional de Contabilidade  | AK_contador  | UNIQUE (crc) |

**5.4 Tabela Advogado**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  INT | NÃO  | x  | x  | |
| oab  | INT  | NÃO  |   |   |x |
| id_coordena  | INT  | SIM  |   |  x | | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idfuncionario |  Chave primária | Identificador do funcionario | PK_advogado | PRIMARY KEY (idfuncionario, oab)  |
|  idfuncionario | Chave estrangeira |  Chave estrangeira referenciando coluna idfuncionario da tabela funcionario |FK_advogado_funcionario	  |  FOREIGN KEY (idfuncionario) REFERENCES funcionario |
|  oab |  Chave candidata  | Indica o registro no Ordem ods Advogados do Brasil  | AK_advogado  | UNIQUE (oab) |
|  id_coordena |  Chave estrangeira | Chave estrangeira referenciando coluna id_coordena da tabela advogado |FK_id_coordenado | FOREIGN KEY (id_coordena) REFERENCES advogado  |

**5.5 Tabela Consulta**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idconsulta |  INT | NÃO  | X  |   | |
| idfuncionario  | INT  | NÃO  |   | X  | |
| pauta  | VARCHAR(45)  | NÃO  |   |   | | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idconsulta |  Chave primária | Identificador da consulta  | PK_consulta | PRIMARY KEY (idconsulta)  |
| idfuncionario  | Chave estrangeira referenciando coluna idfuncionario da tabela funcionario  | Nome do funcionário  |  FK_consulta_funcionario | FOREIGN KEY (idfuncionario) REFERENCES funcionario |


**5.6 Tabela Agenda**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  hora_inicio |  TIME | NÃO  |   |   | X|
| idcliente | INT  | NÃO  | X  |  X |  |
| dia | DATE  | NÃO  |  X |   |  | 
| idconsulta | INT | NÃO  | X  |  X |  | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  dia |  Chave primária | Identificador da consulta  | PK_dia | PRIMARY KEY (dia, idcliente,idconsulta)  |
| idcliente  | Chave estrangeira referenciando coluna idcliente da tabela cliente  | Identificador do cliente  |  FK_agenda_cliente | FOREIGN KEY (idcliente) REFERENCES cliente |
| idconsulta  | Chave estrangeira referenciando coluna idconsulta da tabela consulta  | Identificador da consulta  |  FK_agenda_consulta | FOREIGN KEY (idconsulta) REFERENCES consulta |
| hora_inicio  | Chave candidata  | Indica a hora agendada  | AK_hora_inicio  | UNIQUE (hora_inicio) |

**5.7 Tabela Cliente**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idcliente | INT  | NÃO  |  X |   |  |
| nomeCliente | VARCHAR(45)  | NÃO  |   |   |  |
| rua | VARCHAR(45)  | NÃO  |   |   |  |
| numero | VARCHAR(45)  | NÃO  |   |   |  |
| bairro | VARCHAR(45)  | NÃO  |   |   |  |  |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idcliente |  Chave primária | Identificador do cliente  | PK_idcliente | PRIMARY KEY (idcliente)  |

**5.8 Tabela Fisica**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idcliente | INT  | NÃO  |   | X  |  |
| cpf | BIGINT  | NÃO  |   |   | X |


- Constraints: 

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idcliente |  Chave primária | Identificador do cliente  | PK_cliente_fisico | PRIMARY KEY (idcliente)  |
|  idcliente | Chave estrangeira |  Chave estrangeira referenciando coluna idclienteda tabela cliente | FK_fisico_cliente  |  FOREIGN KEY (idcliente) REFERENCES cliente |
|  cpf |  Chave candidata  | Indica o CPF  | AK_cpf  | UNIQUE (cpf) |
|  cpf |  Check  | Confere se o CPF tem a quantidade correta de números  | CK_cpf  | CHECK		(LEN(cpf) = 11) |

**5.9 Tabela Juridica**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idcliente | INT  | NÃO  |   | X  |  |
| cnpj | BIGINT  | NÃO  |   |   | X |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idcliente |  Chave primária | Identificador do cliente  | PK_cliente_juridico | PRIMARY KEY (idcliente)  |
|  idcliente | Chave estrangeira |  Chave estrangeira referenciando coluna idclienteda tabela cliente | FK_juridica_cleinte  |  FOREIGN KEY (idcliente) REFERENCES cliente |
|  cnpj |  Chave candidata  | Indica o CNPJ  | AK_cnpj  | UNIQUE (cnpj) |
|  cnpj |  Check  | Confere se o CNPJ tem a quantidade correta de números  | CK_cnpj  | CHECK		(LEN(cnpj) = 11) |

**5.10 Tabela Telefone**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| fone | BIGINT  | NÃO  |  X |   |  |
| idcliente | INT  | NÃO  | X  |  X |  |
| tipo | VARCHAR(45)  | NÃO  |   |   |  | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  fone |  Chave primária | Identificador do cliente  | PK_fone | PRIMARY KEY (fone,idcliente)  |
|  idcliente |  Chave estrangeira referenciando coluna idcliente da tabela cliente | Identificador do cliente  | FK_fone_cliente | FOREIGN KEY (idcliente) REFERENCES cliente  |

**5.11 Tabela Gera**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idconsulta |  BIGINT | NÃO  |   | X  | |
| idcliente | INT  | NÃO  |   |  X |  |
| dia | DATE  | NÃO  |  X |   |  |
| idcontrato | BIGINT  | NÃO  |   |  X |  | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  - |  Chave primária | Chave primária  | PK_gera | PRIMARY KEY (idconsulta, idcliente, dia, idcontrato)  |
|  idconsulta |  Chave estrangeira referenciando coluna idconsulta da tabela consulta | Identificador da consulta  | FK_gera_consulta | FOREIGN KEY (idconsulta) REFERENCES consulta  |
| idcliente  | Chave estrangeira referenciando coluna idcliente da tabela cliente  | Identificador do cliente  |  FK_gera_cliente | FOREIGN KEY (idcliente) REFERENCES cliente |
| dia  | Chave rpimária  | Identificador da data  |  PK_dia | PRIMARY KEY (dia)|
| idcontrato  | Chave estrangeira referenciando coluna contrato da tabela contrato  | Identificador do contrato  |  FK_gera_contrato | FOREIGN KEY (idcontrato) REFERENCES contrato |

**5.12 Tabela Contrato**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idcontrato | INT  | NÃO  |  X |   |  |
| numero_contrato | INT  | NÃO  |   |   | X |
| valor | BIGINT  | NÃO  |   |   |  |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idcontrato |  Chave primária | Identificador do contrato  | PK_contrato | PRIMARY KEY (idcontrato)  |
|  numero_contrato |  Chave candidata | Identificador alternativo do contrato  | AK_contrato | UNIQUE (numero_contrato)  |	

**5.13 Tabela Processo**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
|  idprocesso |  BIGINT | NÃO  |  X |   | |
| numProcesso | DECIMAL (38, 0)  | NÃO  |   |   | X |
|  idcontrato |  BIGINT | NÃO  | X  | X  | |
| idvara | INT  | NÃO  | X  |  X |  |
| idjuiz | INT  | NÃO  | X  |  X | |  |



- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idprocesso |  Chave primária | Identificador do processo  | PK_processo | PRIMARY KEY (idprocesso, idcontrato, idvara, idjuiz) |
| idcontrato  | Chave estrangeira referenciando coluna contrato da tabela contrato  | Identificador do contrato  |  FK_processo_contrato | FOREIGN KEY (idcontrato) REFERENCES contrato |
| idvara  | Chave estrangeira referenciando coluna idvara da tabela vara  | Identifica a vara ao qual o processo está vinculado  |  FK_processo_vara | FOREIGN KEY (idvara) REFERENCES vara |
| idjuiz  | Chave estrangeira referenciando coluna idjuiz da tabela juiz  | Identifica o juiz ao qual o processo está vinculado  |  FK_processo_juiz | FOREIGN KEY (idjuiz) REFERENCES juiz |
| numProcesso  | Chave candidata  | Identificação única do processo  |  AK_Processo | UNIQUE		(numProcesso) |
| numProcesso  | Check  | Checa se o número do processo possui a quantidade correta de dígitos  |  CK_numProcesso | CHECK (LEN(numProcesso) = 20)

**5.14 Tabela Vinculado**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idedefensor | int  | NÃO  | X  |  X |  |
| idreu | int  | NÃO  | X  |  X |  | 
| idtestemunha | int  | NÃO  | X  |  X |  | |
| idprocesso | bigint  | NÃO  | X  |  X |  | |
| idvara | int  | NÃO  | X  |  X |  | |
| idjuiz | int  | NÃO  | X  |  X |  | |
| idcontrato | bigint  | NÃO  | X  |  X |  | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
| .  | Chave primária  | Chave primária  |  PK_vinculado	 | PRIMARY KEY (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) |
| iddefensor  | Chave estrangeira referenciando coluna iddefensor da tabela defensor  | Identificador do advogado ou representante judicial do réu  |  FK_vinculado_defensor | FOREIGN KEY (iddefensor) REFERENCES defensor |
| idreu  | Chave estrangeira referenciando coluna idreu da tabela reu  | Identificador do  réu  |  FK_vinculado_reu | FOREIGN KEY (idreu) REFERENCES reu |
| idtestemunha  | Chave estrangeira referenciando coluna idtestemunha da tabela testemunha | Identificador da testemunha  |  FK_vinculado_testemunha | FOREIGN KEY (idtestemunha) REFERENCES testemunha |
| idjuiz  | Chave estrangeira referenciando coluna idjuiz da tabela juiz | Identificador do juiz  |  FK_vinculado_processo_juiz | FOREIGN KEY (idtestemunha) REFERENCES testemunha |
| idvara  | Chave estrangeira referenciando coluna idvara da tabela vara | Identificador da vara  |  FK_vinculado_processo_vara | FOREIGN KEY (idvara) REFERENCES vara |
| idcontrato | Chave estrangeira referenciando coluna idcontrato  da tabela contrato | Identificador do contrato  |  FK_vinculado_processo_contrato | FOREIGN KEY (idcontrato) REFERENCES contrato |

**5.15 Tabela Defensor**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idedefensor | int  | NÃO  | X  |   |  |
| nome | VARCHAR(45)  | NÃO  |   |   |  |
| oab_def | INT  | NÃO  |   |   | X |
| escritorio | VARCHAR(45)  | NÃO  |   |   |  | |


- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
| iddefensor  | Chave primária  | Identificador do advogado ou representante judicial do réu  |  PK_iddefensor | PRIMARY KEY (iddefensor)|
| oab_def  | Chave candidata  | Identificador a identificação profissional do advogado que defende o réu  |  AK_oab_def | UNIQUE (oab_def) |

**5.16 Tabela Réu**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idreu | INT  | NÃO  |  X |   |  |
| nome | VARCHAR(45)  | NÃO  |   |   |  |
| cidade | VARCHAR(45)  | NÃO  |   |   |  |
| rua | VARCHAR(45)  | NÃO  |   |   |  |
| email | INT  | NÃO  |   |   |  |
| telefone | BIGINT  | NÃO  |   |   |  |  |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idreu |  Chave primária | Identificador do reu  | PK_idreu | PRIMARY KEY (idreu)  |

**5.17 Tabela Testemunha**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idtestemunha | INT  | NÃO  |  X |   |  |
| nome | VARCHAR(45)  | NÃO  |   |   | X |
| telefone | BIGINT  | NÃO  |   |   |  |  
| email | INT  | SIM  |   |   |  | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idtestemunha |  Chave primária | Identificador da testemunha  | PK_testemunha | PRIMARY KEY (idtestemunha)  |
|  nome |  Chave candidata | Nome da testemunha  | AK_testemunha | UNIQUE (nome)  |

**5.18 Tabela Juiz**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idjuiz | INT  | NÃO  |  X |   |  |
| nome | VARCHAR(45)  | NÃO  |   |   |  |
| matricula | BIGINT  | NÃO  |   |   |  | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idjuiz |  Chave primária | Identificador do juiz  | PK_juiz | PRIMARY KEY (idjuiz)  |

**5.19 Tabela Vara**

| ATRIBUTO |TIPO  | NULO  | PK  | FK  | AK |
| ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| idvara | INT  | NÃO  |  X |   |  |
| idjuiz | INT  | NÃO  | X  | X  |  |
| num_vara | INT  | NÃO  |   |   | X |
| cidade | VARCHAR(45)  | NÃO  |   |   |  |
| rua | VARCHAR(45)  | NÃO  |   |   |  |
| estado | VARCHAR(45)  | NÃO  |   |   |  | |

- Constraints:

| COLUNA |TIPO  | DESCRIÇÃO  | NOME | EXPRESSÃO
| ------------ | ------------ | ------------ | ------------ | ------------ |
|  idvara |  Chave primária | Identificador da vara  | PK_vara | PRIMARY KEY (idvara, idjuiz)  |
| idjuiz  | Chave estrangeira referenciando coluna idjuiz da tabela juiz  | Identificador do  juiz  |  FK_vara_juiz | FOREIGN KEY (idjuiz) REFERENCES juiz |
| num_vara  | Chave estrangeira referenciando coluna num_vara da tabela vara  | Identificador da vara  |  AK_vara | UNIQUE(num_vara) |
| idjuiz  | Chave estrangeira referenciando coluna idjuiz da tabela juiz  | Identificador do  juiz  |  AK_vara_idjuiz | UNIQUE(idjuiz) |


# 6. Script de Criação do BD

```sql
/***Cria o banco de dados***/ 

CREATE DATABASE ProjetoEscritorio2 

GO 

/***Utiliza o banco de dados criado anteriormente***/ 

USE ProjetoEscritorio2 

GO 

/***Cria tabelas***/ 

CREATE TABLE FUNCIONARIO( 

idfuncionario INT NOT NULL, 

nome VARCHAR(45)	NOT NULL, 

telefone BIGINT NOT NULL, 

email VARCHAR(45) NOT NULl, 

CONSTRAINT PK_funcionario PRIMARY KEY (idfuncionario), 

CONSTRAINT AK_funcionario UNIQUE		(nome) 

) 

CREATE TABLE SECRETARIA( 

idfuncionario INT NOT NULL, 

cfa INT NOT NULL, 

CONSTRAINT PK_secretaria PRIMARY KEY (idfuncionario), 

CONSTRAINT FK_scretaria_funcionario	FOREIGN KEY (idfuncionario) REFERENCES funcionario, 

CONSTRAINT AK_secretaria UNIQUE		(cfa) 

) 

CREATE TABLE CONTADOR( 

idfuncionario INT NOT NULL, 

crc INT NOT NULL, 

CONSTRAINT PK_contador PRIMARY KEY (idfuncionario), 

CONSTRAINT FK_contador_funcionario	FOREIGN KEY (idfuncionario) REFERENCES funcionario, 

CONSTRAINT AK_contador UNIQUE		(crc) 

) 

CREATE TABLE ADVOGADO( 

idfuncionario INT NOT NULL, 

oab INT NOT NULL, 

id_coordenado INT NULL, 

CONSTRAINT PK_advogado PRIMARY KEY (idfuncionario), 

CONSTRAINT FK_advogado_funcionario	FOREIGN KEY (idfuncionario) REFERENCES funcionario, 

CONSTRAINT FK_id_coordenado FOREIGN KEY (id_coordenado)	REFERENCES advogado, 

CONSTRAINT AK_advogado UNIQUE		(oab) 

) 

CREATE TABLE CLIENTE( 

idcliente INT NOT NULL, 

nomeCliente VARCHAR(45)	NOT NULL, 

numero VARCHAR(45)	NOT NULL, 

rua VARCHAR(45)	NOT NULL, 

bairro VARCHAR(45)	NOT NULL, 

CONSTRAINT PK_idcliente PRIMARY KEY (idcliente) 

) 

CREATE TABLE FISICA( 

idcliente INT NOT NULL, 

cpf BIGINT NOT NULL, 

CONSTRAINT PK_cliente_fisico PRIMARY KEY (idcliente), 

CONSTRAINT FK_fisica_cliente FOREIGN KEY (idcliente) REFERENCES cliente, 

CONSTRAINT AK_cpf UNIQUE		(cpf), 

CONSTRAINT CK_cpf CHECK		(LEN(cpf) = 11) 

) 

CREATE TABLE JURIDICA( 

idcliente INT NOT NULL, 

cnpj BIGINT NOT NULL, 

CONSTRAINT PK_cliente_juridico PRIMARY KEY (idcliente), 

CONSTRAINT FK_juridica_cleinte FOREIGN KEY (idcliente) REFERENCES cliente, 

CONSTRAINT AK_cnpj UNIQUE		(cnpj), 

CONSTRAINT CK_cnpj CHECK		(LEN(cnpj) = 14) 

) 

CREATE TABLE TELEFONE( 

idcliente INT NOT NULL, 

fone BIGINT NOT NULL, 

tipo VARCHAR(45) NOT NULL, 

CONSTRAINT PK_fone PRIMARY KEY (fone,idcliente), 

CONSTRAINT FK_fone_cliente FOREIGN KEY (idcliente) REFERENCES cliente 

) 

CREATE TABLE CONSULTA( 

idconsulta BIGINT NOT NULL, 

idfuncionario INT NOT NULL, 

pauta VARCHAR(45)	NOT NULL, 

CONSTRAINT	PK_consulta PRIMARY KEY (idconsulta), 

CONSTRAINT	FK_consulta_funcionario	FOREIGN KEY (idfuncionario) REFERENCES funcionario, 

) 

CREATE TABLE AGENDA( 

hora_inicio TIME NOT NULL, 

idcliente INT NOT NULL, 

dia DATE NOT NULL, 

idconsulta BIGINT NOT NULL, 

CONSTRAINT PK_dia PRIMARY KEY (dia, idcliente,idconsulta), 

CONSTRAINT FK_agenda_cliente FOREIGN KEY (idcliente) REFERENCES cliente, 

CONSTRAINT FK_agenda_consulta FOREIGN KEY (idconsulta) REFERENCES consulta, 

CONSTRAINT AK_hora_inicio UNIQUE		(hora_inicio) 

) 

CREATE TABLE CONTRATO( 

idcontrato BIGINT NOT NULL, 

numero_contrato BIGINT NOT NULL, 

valor BIGINT NOT NULL, 

CONSTRAINT PK_contrato PRIMARY KEY (idcontrato), 

CONSTRAINT AK_contrato UNIQUE		(numero_contrato) 

) 

CREATE TABLE GERA( 

idconsulta BIGINT NOT NULL, 

idcliente INT NOT NULL, 

dia DATE NOT NULL, 

idcontrato BIGINT NOT NULL, 

CONSTRAINT	PK_gera PRIMARY KEY (idconsulta, idcliente, dia, idcontrato), 

CONSTRAINT	FK_gera_consulta FOREIGN KEY (idconsulta)	REFERENCES consulta, 

CONSTRAINT	FK_gera_cliente FOREIGN KEY (idcliente)		REFERENCES cliente, 

CONSTRAINT	FK_gera_dia FOREIGN KEY (dia)		REFERENCES agenda, 

CONSTRAINT	FK_gera_contrato FOREIGN KEY (idcontrato)   REFERENCES contrato 

) 

CREATE TABLE DEFENSOR( 

iddefensor INT NOT NULL, 

nome VARCHAR(45)	NOT NULL, 

oab_def INT NOT NULL, 

escritorio VARCHAR(45)	NOT NULL, 

CONSTRAINT PK_defensor PRIMARY KEY (iddefensor), 

CONSTRAINT AK_defensor UNIQUE		(oab_def) 

) 

CREATE TABLE REU( 

idreu INT NOT NULL, 

nome VARCHAR(45)	NOT NULL, 

cidade VARCHAR(45)	NOT NULL, 

rua VARCHAR(45)	NOT NULL, 

email VARCHAR(45)			NOT NULL, 

telefone	BIGINT NOT NULL, 

CONSTRAINT	PK_reu	PRIMARY KEY (idreu) 

) 

CREATE TABLE TESTEMUNHA( 

idtestemunha	INT NOT NULL, 

nome VARCHAR(45)	NOT NULL, 

telefone BIGINT NOT NULL, 

email VARCHAR(45), 

CONSTRAINT PK_testemunha	PRIMARY KEY (idtestemunha), 

) 

CREATE TABLE JUIZ( 

idjuiz INT NOT NULL, 

nome VARCHAR(45)	NOT NULL, 

matricula	BIGINT NOT NULL, 

CONSTRAINT PK_juiz PRIMARY KEY (idjuiz) 

) 

CREATE TABLE VARA( 

idvara INT NOT NULL, 

idjuiz INT NOT NULL, 

num_vara INT NOT NULL, 

cidade VARCHAR(45)	NOT NULL, 

rua VARCHAR(45)	NOT NULL, 

estado VARCHAR(45)	NOT NULL, 

CONSTRAINT	PK_vara PRIMARY KEY (idvara, idjuiz), 

CONSTRAINT	FK_vara_juiz FOREIGN KEY (idjuiz) REFERENCES juiz, 

CONSTRAINT	AK_vara UNIQUE		(num_vara), 

CONSTRAINT	AK_vara_idjuiz UNIQUE		(idjuiz) 

) 

CREATE TABLE VINCULADO( 

iddefensor INT NOT NULL, 

idprocesso BIGINT NOT NULL, 

idreu INT NOT NULL, 

idtestemunha INT NOT NULL, 

idcontrato BIGINT NOT NULL, 

idvara INT NOT NULL, 

idjuiz INT NOT NULL, 

CONSTRAINT	PK_vinculado PRIMARY KEY (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz), 

CONSTRAINT	FK_vinculado_defensor FOREIGN KEY (iddefensor) REFERENCES defensor, 

CONSTRAINT	FK_vinculado_processo FOREING KEY (idprocesso) REFERENCES processo, 

CONSTRAINT	FK_vinculado_processo_contrato FOREING KEY (idcontrato) REFERENCES processo, 

CONSTRAINT	FK_vinculado_processo_vara	FOREING KEY (idvara) REFERENCES processo, 

CONSTRAINT	FK_vinculado_processo_juiz	FOREING KEY (idjuiz) REFERENCES processo, 

CONSTRAINT	FK_vinculado_reu FOREIGN KEY (idreu) REFERENCES reu, 

CONSTRAINT	FK_vinculado_testemunha FOREIGN KEY (idtestemunha) REFERENCES testemunha 

) 

CREATE TABLE PROCESSO( 

idprocesso BIGINT	NOT NULL, 

numProcesso DECIMAL (38, 0)	NOT NULL, 

idcontrato BIGINT	NOT NULL, 

idvara INT NOT NULL, 

idjuiz INT NOT NULL, 

CONSTRAINT	PK_processo PRIMARY KEY (idprocesso, idcontrato, idvara, idjuiz), 

CONSTRAINT	FK_processo_contrato FOREIGN KEY (idcontrato	)   REFERENCES contrato, 

CONSTRAINT	FK_processo_vara FOREIGN KEY (idvara) REFERENCES vara, 

CONSTRAINT	FK_processo_juiz FOREIGN KEY (idjuiz) REFERENCES juiz, 

CONSTRAINT	AK_Processo UNIQUE		(numProcesso), 

CONSTRAINT	CK_numProcesso CHECK		(LEN(numProcesso) = 20) 

)
```

# 7. Script de povoamento do BD

```sql
/**Tabela Funcionario**/
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (1, 'Nancee Parkman', 1315281029, 'nparkman0@sogou.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (2, 'Maxy Bartosik', 8042535267, 'mbartosik1@nsw.gov.au');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (3, 'Hazel McCoughan', 1102228562, 'hmccoughan2@cnet.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (4, 'Phebe Willimot', 5589997363, 'pwillimot3@newsvine.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (5, 'Kacy MacBarron', 4767062769, 'kmacbarron4@theatlantic.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (6, 'Consalve McCallister', 6603222874, 'cmccallister5@ameblo.jp');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (7, 'Cazzie Warke', 9293145284, 'cwarke6@posterous.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (8, 'Andreana Chaudron', 3705492937, 'achaudron7@instagram.com');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (9, 'Tymothy Edgeworth', 9067062679, 'tedgeworth8@hhs.gov');
insert into FUNCIONARIO (idfuncionario, nome, telefone, email) values (10, 'Nancee Prichet', 5457198655, 'nprichet9@livejournal.com');

/**Tabela Secretaria**/
insert into SECRETARIA (idfuncionario, cfa) values (1, 847);
insert into SECRETARIA (idfuncionario, cfa) values (2, 622);


/**Tabela Contador**/
insert into CONTADOR (idfuncionario, crc) values (3, 1208);
insert into CONTADOR (idfuncionario, crc) values (4, 1229);

/**Tabela Advogado**/
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (5, 20831, NULL);
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (6, 17156, 5);
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (7, 23056, 5);
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (8, 22430, 5);
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (9, 23328, 5);
insert into ADVOGADO (idfuncionario, oab, id_coordenado) values (10, 22717, 5);

/**Tabela Cliente**/
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (1, 'Lelia McNelly', '2098', 'Eggendart Drive', 'Torre');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (2, 'Sherlock Bechley', '1001', 'Marquette Crossing', 'Centro');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (3, 'Janenna Maddaford', '1912', 'Moulton Court', 'Brisamar');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (4, 'Lucy Overstreet', '110', 'Gerald Hill', 'Altiplano');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (5, 'Lita Treagus', '3002', 'Grasskamp Drive', 'Centro');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (6, 'Creusa Marcelino', '9987', 'Jagua street', 'Jaguaribe');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (7,'Kirestin Franco', '3987','Consectetuer Av.','Manaira');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (8,'Christian Gregory','305', 'Mauris, Av.','Bessa');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (9,'Nadine Morton', '795', 'Nibh. St.','Centro');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (10,'Vladimir Orr', '9112', 'Eu Ave','Cabo Branco');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (11,'Anastasia Small','973', 'Accumsan Rd.','Altiplano');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (12,'Madonna Gilbert','23', 'Luctus Ave','Manaira');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (13,'Clinton Conley','7875', 'Fusce St.','Tambaú');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (14,'Wilma Flowers','88', 'Taner, Street','Tambia');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (15,'Belle Anthony','2150', 'In Street','Manaira');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (16,'Ralph House','173627', 'Curabitur Avenue','Miramar');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (17,'Fleur Vang','8038231', 'Ullamcorper St.','Centro');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (18,'Odette Park','9841', 'Nunc Avenue','Altiplano');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (19,'Addison Cox','2420', 'Lorem Road','Cabedelo');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (20,'Hop Kaufman','413', 'Neque Av.','Jaguaribe');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (21,'Cleo Palmer','9160', 'Augue Road','Cabedelo');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (22,'Cedric Hart','757', 'Consequat Rd.','Miramar');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (23,'Janna White','8965', 'Pede. Street','Bessa');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (24,'Quinn Salazar','2898', 'Veludo, Av.','Cabo Branco');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (25,'Kareem Rhodes','4517', 'Cras Av.','Jaguaribe');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (26,'Heather Lewis','829', 'Sed Road','Centro');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (27,'Hayley Newman','6636', 'Augue Avenue','Torre');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (28,'Rajah Sears','3556', 'Est, Rd.','Bancarios');
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (29,'Thomas Alston','6928', 'Dictum. Av.','Castelo Branco'); 
insert into CLIENTE (idcliente, nomeCliente, numero, rua, bairro) values (30,'Kerry Love','9376', 'Ultrices. Av.','Centro');


/**Tabela Fisica**/
insert into FISICA (idcliente, cpf) values (1, 84138701001);
insert into FISICA (idcliente, cpf) values (2, 98289648448);
insert into FISICA (idcliente, cpf) values (3, 94002059022);
insert into FISICA (idcliente, cpf) values (7, 84136781001);
insert into FISICA (idcliente, cpf) values (8, 98289644567);
insert into FISICA (idcliente, cpf) values (9, 10092059022);
insert into FISICA (idcliente, cpf) values (10, 51067301001);
insert into FISICA (idcliente, cpf) values (11, 45089648487);
insert into FISICA (idcliente, cpf) values (12, 68900205917);
insert into FISICA (idcliente, cpf) values (13, 84138712987);
insert into FISICA (idcliente, cpf) values (14, 12289648448);
insert into FISICA (idcliente, cpf) values (15, 74502059022);


/**Tabela Juridica**/
insert into JURIDICA (idcliente, cnpj) values (4, 36808061000127);
insert into JURIDICA (idcliente, cnpj) values (5, 70897293000137);
insert into JURIDICA (idcliente, cnpj) values (6, 50897293100137);
insert into JURIDICA (idcliente, cnpj) values (16,43789123000101);
insert into JURIDICA (idcliente, cnpj) values (17,43123654000101);
insert into JURIDICA (idcliente, cnpj) values (18,43524617000101);
insert into JURIDICA (idcliente, cnpj) values (19,32123456000101);
insert into JURIDICA (idcliente, cnpj) values (20,32321987000101);
insert into JURIDICA (idcliente, cnpj) values (21,21432567000101);
insert into JURIDICA (idcliente, cnpj) values (22,21123456000101);
insert into JURIDICA (idcliente, cnpj) values (23,21987543000101);
insert into JURIDICA (idcliente, cnpj) values (24,22123456000101);
insert into JURIDICA (idcliente, cnpj) values (25,22321654000101);
insert into JURIDICA (idcliente, cnpj) values (26,22987456000101);
insert into JURIDICA (idcliente, cnpj) values (27,17123456000101);
insert into JURIDICA (idcliente, cnpj) values (28,17567234000101);
insert into JURIDICA (idcliente, cnpj) values (29,15123456000101);
insert into JURIDICA (idcliente, cnpj) values (30,98456123000101);

/**Tabela Telefone**/
insert into TELEFONE (idcliente, fone, tipo) values (1, '1212265854', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (2, '6143429669', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (3, '6474226373', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (4, '5107573673', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (5, '6074774231', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (13,'7920308418', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (21,'9911499223', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (15,'7916686625', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (17,'5978228536', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (22,'6931534430', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (5, '4985754502', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (24,'8925031371', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (25,'9962329511', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (21,'4974238321', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (24,'9926384574', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (21,'4985029554', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (21,'4244542514', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (20,'4931947288', 'Fax' );
insert into TELEFONE (idcliente, fone, tipo) values (13,'9915051456', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (7, '4983274310', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (12,'9975919389', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (12,'9993087536', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (8, '9906554163', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (6, '4928008514', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (10,'4948363318', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (22,'9949290047', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (4, '4971460353', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (1, '4932553537', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (29,'9946562784', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (18,'9262650121', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (14,'9938096403', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (19,'4961397733', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (16,'4945418773', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (12,'4983592596', 'fax');
insert into TELEFONE (idcliente, fone, tipo) values (25,'9942474476', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (16,'9917946816', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (20,'4900314031', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (12,'9908291039', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (25,'4971771142', 'Fax');
insert into TELEFONE (idcliente, fone, tipo) values (3, '4977116849', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (10,'9989617796', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (10,'9963452725', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (24,'4993984535', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (23,'9884831445', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (12,'4876393782', 'Fixo');
insert into TELEFONE (idcliente, fone, tipo) values (26,'9810828040', 'Celular');
insert into TELEFONE (idcliente, fone, tipo) values (18,'9897171529', 'Celular');

/**Tabela Consulta**/
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (502, 5, 'Inventário');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (687, 6, 'Inventário');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (105, 7, 'Defesa Criminal');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (278, 6, 'Penhora');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (383, 8, 'Defesa Criminal');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (455, 5, 'Inventário');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (569, 5, 'Penhora');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (150, 7, 'Defesa Criminal');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (467, 6, 'Penhora');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (210, 10, 'Defesa Criminal');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (42, 7, 'Inventário');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (59, 6, 'Penhora');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (198, 7, 'Defesa Criminal');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (314, 6, 'Penhora');
insert into CONSULTA (idconsulta, idfuncionario, pauta) values (256, 10, 'Defesa Criminal');

/**Tabela Agenda**/
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('7:33', 1, '2019-05-15', 502);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('10:04', 2, '2020-05-31', 687);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('8:54', 3, '2019-10-30', 105);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('9:59', 4, '2019-07-11', 278);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('8:05', 5, '2019-10-04', 383);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('16:15', 14,'2019-06-18', 455);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('9:15', 25,'2019-06-20', 569);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('16:16', 14,'2019-06-08', 150);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('13:50', 12,'2019-10-20', 467);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('13:29', 21,'2019-04-26', 210);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('8:09', 5, '2019-10-03', 42);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('16:00', 14,'2019-06-27', 59);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('10:15', 25,'2019-06-01', 198);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('14:00', 14,'2019-06-07', 314);
insert into AGENDA (hora_inicio, idcliente, dia, idconsulta) values ('15:30', 12,'2019-10-19', 256);


/**Tabela Contrato**/

insert into CONTRATO (idcontrato, numero_contrato, valor) values (95, 1000235, 150000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (257, 1000257, 78000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (101, 1000784, 900);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (112, 1000001, 76900);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (96, 1000425, 12300);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (20, 1000238, 190000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (78, 1000258, 75000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (150, 1000785, 9000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (125, 1000000, 59500);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (268, 1000426, 12000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (52, 1000239, 50000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (278, 1000259, 60000);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (145, 1000786, 1900);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (225, 1000003, 37500);
insert into CONTRATO (idcontrato, numero_contrato, valor) values (98, 1000427, 123000);


/**Tabela Gera**/
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (278, 4, '2019-05-15', 95);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (105, 3, '2020-05-31', 257);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (687, 2, '2019-10-30', 101);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (502, 1, '2019-07-11', 112);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (383, 5, '2019-10-04', 96);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (455, 4, '2019-06-18', 20);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (150, 3, '2019-06-20', 78);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (569, 2, '2019-06-08', 150);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (467, 1, '2019-10-20', 125);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (210, 5, '2019-04-26', 268);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (42, 4,  '2019-10-04', 52);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (59, 3,  '2019-06-27', 278);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (198, 2, '2019-06-01', 145);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (314, 1, '2019-06-07', 225);
insert into GERA (idconsulta, idcliente, dia, idcontrato) values (256, 5, '2019-10-20', 98);

/**Tabela Defensor**/
insert into DEFENSOR (iddefensor, nome, oab_def, escritorio) values (74, 'Melissa Golton', 7944, 'Demizz');
insert into DEFENSOR (iddefensor, nome, oab_def, escritorio) values (75, 'Monique Pacquet', 9558, 'Flashset');
insert into DEFENSOR (iddefensor, nome, oab_def, escritorio) values (76, 'Darin Sline', 9817, 'Brainsphere');
insert into DEFENSOR (iddefensor, nome, oab_def, escritorio) values (77, 'Bearnard Ungerechts', 8121, 'Thoughtworks');
insert into DEFENSOR (iddefensor, nome, oab_def, escritorio) values (78, 'Sam Bugg', 4196, 'InnoZ');

/**Tabela Reu**/
insert into REU (idreu, nome, cidade, rua, email, telefone) values (151, 'Breena Gallemore', 'Bontoc', 'Porter', 'errofdp@odeioisso.com', 2294411741);
insert into REU (idreu, nome, cidade, rua, email, telefone) values (152, 'Holden Oxherd', 'Yurkivka', 'Sullivan', 'hoxherd1@trellian.com', 8382537519);
insert into REU (idreu, nome, cidade, rua, email, telefone) values (200, 'Sioux Peeters', 'Kisangani', 'Pennsylvania', 'speeters2@yandex.ru', 4546947732);
insert into REU (idreu, nome, cidade, rua, email, telefone) values (173, 'Evita Demeter', 'Fajões', 'Holmberg', 'edemeter3@i2i.jp', 1129482098);
insert into REU (idreu, nome, cidade, rua, email, telefone) values (168, 'Kata Bates', 'Krajan Kinanti', 'Spaight', 'kbates4@house.gov', 8463280940);

/**Tabela Testemunha**/
insert into TESTEMUNHA (idtestemunha, nome, telefone, email) values (294, 'Neddy Baty', '5474789283', 'nbaty0@amazon.de');
insert into TESTEMUNHA (idtestemunha, nome, telefone, email) values (234, 'Jo Trusler', '1764623598', 'jtrusler1@reddit.com');
insert into TESTEMUNHA (idtestemunha, nome, telefone, email) values (263, 'Chilton Boddington', '2372880091', 'cboddington2@tumblr.com');
insert into TESTEMUNHA (idtestemunha, nome, telefone, email) values (216, 'Rey Neilus', '2873895518', 'rneilus3@yolasite.com');
insert into TESTEMUNHA (idtestemunha, nome, telefone, email) values (213, 'Erda Galland', '4703840899', 'egalland4@japanpost.jp');

/**Tabela Juiz**/
insert into JUIZ (idjuiz, nome, matricula) values (400, 'Wylie Yeatman', 19516);
insert into JUIZ (idjuiz, nome, matricula) values (240, 'Calli Tuiller', 16167);
insert into JUIZ (idjuiz, nome, matricula) values (450, 'Nettle Andrzejczak', 16488);
insert into JUIZ (idjuiz, nome, matricula) values (460, 'Jecho McGeraghty', 17044);
insert into JUIZ (idjuiz, nome, matricula) values (230, 'Crosby Roddell', 17186);

/**Tabela Vara**/
insert into VARA (idvara, idjuiz, num_vara, cidade, rua, estado) values (500, 400, 1, 'Orekhovo-Zuyevo', 'Northfield', 'PB');
insert into VARA (idvara, idjuiz, num_vara, cidade, rua, estado) values (501, 240, 2, 'Hengjian', 'Warrior', 'SE');
insert into VARA (idvara, idjuiz, num_vara, cidade, rua, estado) values (502, 450, 3, 'Saryaghash', 'Mitchell', 'SP');
insert into VARA (idvara, idjuiz, num_vara, cidade, rua, estado) values (503, 460, 4, 'Cahabón', 'North', 'RJ');
insert into VARA (idvara, idjuiz, num_vara, cidade, rua, estado) values (504, 230, 5, 'Sukamaju', 'Heffernan', 'AM');

/**Tabela Vinculado**/
insert into VINCULADO (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) values (74, 989, 151, 263, 95, 500, 400);
insert into VINCULADO (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) values (76, 898, 152, 216, 257, 501, 240);
insert into VINCULADO (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) values (75, 797, 200, 234, 101, 502, 450);
insert into VINCULADO (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) values (74, 696, 173, 294, 112, 503, 460);
insert into VINCULADO (iddefensor, idprocesso, idreu, idtestemunha, idcontrato, idvara, idjuiz) values (78, 595, 168, 213, 225, 504, 230);

/**Tabela Processo**/
insert into PROCESSO (idprocesso, numProcesso, idcontrato, idvara, idjuiz) values (989, 18607278320198152001, 95, 500, 400);
insert into PROCESSO (idprocesso, numProcesso, idcontrato, idvara, idjuiz) values (898, 18507278320198152001, 257, 501, 240);
insert into PROCESSO (idprocesso, numProcesso, idcontrato, idvara, idjuiz) values (797, 18707278320198152001, 101, 502, 450);
insert into PROCESSO (idprocesso, numProcesso, idcontrato, idvara, idjuiz) values (696, 18807278320198152001, 112, 503, 460);
insert into PROCESSO (idprocesso, numProcesso, idcontrato, idvara, idjuiz) values (595, 18907278320198152001, 225, 504, 230);
```

# 8. Scripts de alterações

```sql
/**Modifica OAB de um advogado**/
UPDATE advogado
SET oab = 20209
WHERE idfuncionario = 9

/**Modifica telefone e tipo**/
UPDATE telefone
SET fone = 2007573677, tipo = Fixo
WHERE idclient = 4 AND tipo = Celular

/**Deleta clientes sem agendamento**/
DELETE FROM cliente
WHERE idcliente NOT IN (SELECT idcliente 
		    FROM AGENDA)

/**Deleta funcionario**/
DELETE FROM funcionario
WHERE idfuncionario = 2

/** IN **/
SELECT * FROM TELEFONE
WHERE tip IN ('Fixo','Fax');


/** NOT IN **/
SELECT * FROM TELEFONE
WHERE tipo NOT IN ('Celular');

/** BETWEEN **/
SELECT * FROM CONTRATO
WERE valor BETWEEN '50000' AND '100000';

/** NOT BETWEEN **/
SELECT * FROM AGENDA
WHERE CAST(dia AS DATE) NOT BETWEEN '2019-10-01' AND '2019-12-31';

/** IS NULL **/
SELECT * FROM ADVOGADO
WHERE id_coordenado IS NULL;

/** IS NOT NULL **/
SELECT * FROM ADVOGADO
WHERE id_coordenado IS NOT NULL;

/** LIKE **/
SELECT * FROM CLIENTE
WHERE bairro LIKE 'b%';

/** NOT LIKE **/
SELECT * FROM JUIZ
WHERE nome NOT LIKE 'c%';

/** ORDER BY **/
SELECT * FROM CLIENTE
WHERE BAIRRO IS 'Centro'
ORDER BY name;

/** COUNT **/
SELECT COUNT(nome)
FROM FUNCIONÁRIO
WHERE nome LIKE 'c%';

/** SUM **/
SELECT SUM(valor) AS total
FROM CONTRATO;

/** AVG **/
SELECT AVG(valor) AS valor_medio
FROM CONTRATO;

/** MAX **/
SELECT MIN(valor) AS valor_max
FROM CONTRATO;

/** MIN **/
SELECT MIN(valor) AS valor_minimo
FROM CONTRATO;

/** GROUP BY **/
SELECT * FROM CONTRATO
GROUP BY Bairro
ORDER BY nome;


/** HAVING **/
SELECT COUNT(idcliente), Bairro
FROM CLIENTE
GROUP BY Bairro
HAVING COUNT(idcliente) >= 3;

/** INNER JOIN **/
SELECT CLIENTE.nome, GERA.idcontrato, CONTRATO.numerocontrato
FROM CLIENTE
INNER JOIN GERA
ON CLIENTE.idcontrato = GERA.idcontrato
ORDER BY CLIENTE.nome;

/** LEFT JOIN **/
SELECT PROCESSO.numProcesso, REU.idreu
FROM PROCESSO
LEFT JOIN PROCESSO 
ON PROCESSO.idreu = REU.idreu
ORDER BY PROCESSO.numProcesso;

/** RIGHT JOIN **/
SELECT PROCESSO.numProcesso, TESTEMUNHA.idtestemunha
FROM PROCESSO
RIGHT JOIN TESTEMUNHA ON PROCESSO.idtestemunha = TESTEMUNHA.idtestemunha
ORDER BY PROCESSO.numProcesso;

/** FULL JOIN **/
SELECT PROCESSO.numProcesso, DEFENSOR.iddefensor
FROM PROCESSO
FULL OUTER JOIN PROCESSO ON PROCESSO.iddefensor = DEFENSOR.iddefensor
ORDER BY PROCESSO.numProcesso;

/** SUBCONSULTA **/
SELECT idcliente, nome, bairro
FROM CLIENTE
WHERE idtelefone IN (SELECT idtelefone FROM TELEFONE
WHERE idtelefone = (SELECT tipo FROM TELEFONE
WHERE tipo = 'Celular'))
```
