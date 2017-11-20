# TRABALHO 01:  Título do Trabalho
Trabalho desenvolvido durante a disciplina de BD1

# Sumário

### 1. COMPONENTES<br>
Integrantes do grupo<br>
Renato da Silva Bellumat:renato.bellumat@hotmail.com<br>
Luciano Ananias Barboza Junior:luciano.ananias.40@gmail.com<br>


### 2.INTRODUÇÃO E MOTIVAÇAO<br>
O projeto DestinoES basea-se em um aplicativo de busca de pontos turísticos e hotéis de locais do estado do Espírito Santo. Decidimos desenvolver este trabalho, pois se encaixa muito bem na disciplina de banco de dados tendo em vista que temos que cadastrar vários usuários, pontos turísticos e hotéis disponíveis, além de podermos incentivar o turismo capixaba, mostrando lugares incríveis  que nem todo mundo tem conhecimento e que caiba no orçamento.

### 3.MINI-MUNDO<br>

O App se basearia em pessoas que tenha uma determinada quantia de dinheiro e esteja disposta à fazer uma viagem ou conhecer locais Capixabas com essa quantia. No sistema a pessoa indica uma certa quantia que deseja gastar e o aplicativo provém destinos em terras Capixabas que o mesmo pode chegar usando essa quantia determinada. A reserva da Pousada e afins não são disponibilizadas pelo aplicativo, o objetivo principal é apenas mostrar as opções de destinos dentro do orçamento. O sistema também calculará o valor do deslocamento por carro e por ônibus(caso o destino possua uma distância maior) assim como a distância do local de origem para o local de destino que será disponibilizado por um aplicativo de mapas como por exemplo o Google Maps.


### 4.RASCUNHOS BÁSICOS DA INTERFACE (MOCKUPS)<br>

[Mockup](https://github.com/destinoespiritosanto/trab01/blob/master/Destinos%20ES.pdf "mockup")

#### 4.1 TABELA DE DADOS DO SISTEMA:
   [Tabela](https://github.com/destinoespiritosanto/trab01/blob/master/Tabela%20de%20dados.ods)
    
    
#### 4.2 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?
   Poderá fornecer informações sobre a pousada e o local onde o usuário deseja visitar e relatórios de dados como mais pesquisados e        mais bem avaliados.
   Lista dos relatórios:
   -Novos usuários
   -Mais pesquisados
   -Melhores avaliados
   -Média de preço pesquisado
   -Média de idade
   -Média da gasolina
   -Distancia percorrida pelo usuário
    
>## Marco de Entrega 01 em: (Data definida no cronograma)<br>

### 5.MODELO CONCEITUAL<br>
        
![Alt text](https://github.com/destinoespiritosanto/trab01/blob/master/mapa_conceitual.PNG "Modelo Conceitual")

        
    
#### 5.1 Validação do Modelo Conceitual
    [Grupo01]: [Nomes dos que participaram na avaliação]
    [Grupo02]: [Nomes dos que participaram na avaliação]

#### 5.2 DECISÕES DE PROJETO
  
    
    a) cd_usuario: valor serial pois cada usuario terá um codigo inteiro crescente;
    b) nm_usuario: campo varchar para ter acesso ao nome do usuário;
    c) dt_nascimento: tipo date com finalidade de obter informações do usuário (idade);
    d) email_usuario: tipo varchar com finalidade de obter uma forma de contatar o usuário;
    e) senha_usuario: tipo varchar codigo pessoal para utilizar o aplicativo;
    f) cd_cidade: tipo serial para armazenar o código da cidade de forma crescente;
    g) nm_cidade: tipo varchar acesso do nome da cidade para pesquisa do usuário;
    h) cd_hp: tipo serial para armazenar o código do hotel/pousada;
    i) nm_hp: tipo varchar para ter acesso ao nome do hotel/pousada;
    j) cd_bairro: tipo serial para servir de informação à um endereço;
    k) nm_bairro: tipo varchar para acesso ao nome do bairro;
    l) cd_rua: tipo serial para servir de informação à um endereço;
    m) nm_rua: tipo varchar para servir de informação do nome da rua;
    n) preco_gasolina: tipo money para calcular gastos com deslocamento;
    o) cd_pt: tipo serial para armazenar código do ponto turístico;
    p) nm_pt: tipo varchar para armazenar nome do ponto turístico;
    
    
#### 5.3 DESCRIÇÃO DOS DADOS  
   Usuário: Tabela que armazena informações relativas ao usuário como nome, código e etc;
   Pesquisa: Campo que relaciona o usuário com o que ele deseja;
   Hotel/Pousada: Tabela com informações sobre pousadas cadastradas no aplicativo.
   Cidade: Tabela com informações sobre cidades do Espírito Santo com algum hotel/pousada cadastrado.
   Gasolina: Tabela com informações de preço com finalidade de informar valores gastos com deslocamento.
   Ponto Turístico: Tabela com informações de pontos turísticos de uma cidade em específico.

### 6	MODELO LÓGICO<br>
        a) inclusão do modelo lógico do banco de dados
        b) verificação de correspondencia com o modelo conceitual 
        (não serão aceitos modelos que não estejam em conformidade)

>## Marco de Entrega 02 em: (Data definida no cronograma)<br>

### 7	MODELO FÍSICO<br>
        a) inclusão das instruções de criacão das estruturas DDL 
        (criação de tabelas, alterações, etc..)
          
        
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
#### 8.1 DETALHAMENTO DAS INFORMAÇÕES
   CREATE TABLE usuario(
   
   cd_usuario serial not null, 
   nm_usuario varchar(100) not null,
   dt_nascimento date,
   email_usuario varchar(50),
   senha_usuario varchar(18) not null,
   cd_cidade int not null
   PRIMARY KEY (cd_usuario)
   FOREIGN KEY cd_cidade REFERENCES cidade(cd_cidade));

CREATE TABLE cidade(
   cd_cidade serial not null,
   nm_cidade char(20) not null
   PRIMARY KEY (cd_cidade));



CREATE TABLE hotel_pousada(
   cd_hp serial not null,
   nm_hp varchar(100),
   PRIMARY KEY(cd_hp));

CREATE TABLE bairro(
  cd_bairro serial not null,
  nm_bairro varchar(50) not null,
  cd_cidade int not null,
  FOREIGN KEY cd_cidade REFERENCES cidade(cd_cidade));

CREATE TABLE rua(
  cd_rua serial not null,
  nm_rua varchar(100) not null,
  cd_bairro int not null,
  FOREIGN KEY cd_bairro REFERENCES bairro(cd_bairro));

CREATE TABLE pontos_turisticos(
   
  cd_pt serial not null,
  nm_pt varchar(200),
  cd_cidade int not null,
  PRIMARY KEY (cd_pt),
  FOREIGN KEY cd_cidade REFERENCES cidade(cd_cidade));

CREATE TABLE gasolina(
  preco_gasolina money not null
  cd_cidade int not null
  FOREIGN KEY cd_cidade REFERENCES cidade(cd_cidade));

#### 8.2 INCLUSÃO DO SCRIPT PARA CRIAÇÃO DE TABELA E INSERÇÃO DOS DADOS
INSERT INTO usuario(nm_usuario,dt_nascimento,email_usuario,senha_usuario,cd_cidade);

VALUES('Leonardo','1995-12-31','leonardo.24@exemple.com','leo123','2'),
(Renato B','1992
-04-24','renato.24@exemple.com','re123','2'),
('Luciano Barboza','1996-02-
20','luciano.24@exemple.com','lu123','1'),
('Ana Carolina','1994-04-
22','ana.24@exemple.com','ana123,'5'),
('Matheus Barbosa','1994-04-
29','matheus.24@exemple.com','mat123','2'),
('Lucas Bellumat',1995-09-
03','lucas.24@exemple.com','luc123','5'),
('Rodrigo Bellumat','1994-01-
12','rodrigo.24@exemple.com','rod123','1'),
('Sarah Rizzo','1998-04-
25','sarah.20@exemple.com','sa123',7'),
('Jéssica Lirio','1992-05-
02','jessica.24@exemple.com','je123','3'),
('Lynda Silva','1993-11-
01','lynda.24@exemple.com','ly123','2');

INSERT INTO cidade(nm_cidade);
VALUES('Guarapari'),
('Vitoria'),('Domingos Martins'),('São Mateus'),
('Itaúnas'),
('Piúma'),('Colatina'),
('Marechal Floriano'),('Itarana'),('Linhares');

INSERT INTO hotel_pousada(cd_hp,nm_hp);
VALUES('Hotel Maryland'),
('Ibis Hotel'),('Maratu'),('Hotel Budapeste'),('Paradise'),
('Aruan'),('Hotel de Colatina'),('Cacatua'),('Conrado'),
('Palace Hotel');

INSERT INTO pontos_turisticos(cd_cidade,nm_pt);
VALUES('1','Praia do Morro','Praia aberta à todos os públicos, sem preço e com vários restaurantes.')
('2','Pedra Da Cebola', 'Aberto de 5:00 às 22:00m sem preço. Um passeio ecológico.'),('3','Pedra Azul','Aberto das 8:00 às 17:00, entrada gratuita e passeio ecológico.'),
('4','Guriri','Praia aberta à todos os públicos, sem preço e com vários restaurantes ao longo da orla.'),('5','Dunas','Aberto à todos públicos e gratuito.'),
('6','Praia 
de Piuma','Praia aberta à todos públicos, sem preço e com vários restaurantes.'),('7','Catedral Sagrado Coraçao','Aberta à todos os públicos das 8:00 às 18:00 e entrada gratuita),
('8','Zoo Park da Motanha','Aberto de 9:00 às 16:00 e custo da entrada de 13,50 reais.'),
('Capela de Santa Luzia'),('Reserva 
Biologica')

#### 8.3 INCLUSÃO DO SCRIPT PARA EXCLUSÃO DE TABELAS EXISTENTES, CRIAÇÃO DE TABELA NOVAS E INSERÇÃO DOS DADOS
        a) Junção dos scripts anteriores em um único script 
        (Drop table + Create de tabelas e estruturas de dados + dados a serem inseridos)
        b) Criar um novo banco de dados para testar a restauracao 
        (em caso de falha na restauração o grupo não pontuará neste quesito)
        c) formato .SQL


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>
    OBS: Incluir para cada tópico as instruções SQL + imagens (print da tela) mostrando os resultados.<br>
#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>
#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>
#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E CAMPOS RENOMEADOS (Mínimo 6)
     a) Criar no mínimo 2 com operadores lógicos
     b) Criar no mínimo 2 com operadores aritméticos
     c) Criar no mínimo 2 com operação de renomear campo
#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE (Mínimo 4) <br>

>## Marco de Entrega 03 em: (Data definida no cronograma)<br>
    
#### 9.5	ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
#### 9.6	CONSULTAS COM JUNÇÃO E ORDENAÇÃO (Mínimo 6)<br>
        a) Uma junção que envolva todas as tabelas possuindo no mínimo 3 registros no resultado
        b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho
#### 9.7	CONSULTAS COM GROUP BY E FUNÇES DE AGRUPAMENTO (Mínimo 6)<br>
#### 9.8	CONSULTAS COM LEFT E RIGHT JOIN (Mínimo 4)<br>
#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
        a) Uma junção que envolva Self Join
        b) Outras junções com views que o grupo considere como sendo de relevante importância para o trabalho
#### 9.10	SUBCONSULTAS (Mínimo 3)<br>
### 10	ATUALIZAÇÃO DA DOCUMENTAÇÃO DOS SLIDES PARA APRESENTAÇAO FINAL (Mínimo 6 e Máximo 10)<br>
### 11	TUTORIAL COMPLETO DE PASSOS PARA RESTAURACAO DO BANCO E EXECUCAO DE PROCEDIMENTOS ENVOLVIDOS NO TRABALHO PARA OBTENÇÃO DOS RESULTADOS<br>
        a) Outros grupos deverão ser capazes de restaurar o banco 
        b) executar todas as consultas presentes no trabalho
        c) executar códigos que tenham sido construídos para o trabalho 
        d) realizar qualquer procedimento executado pelo grupo que desenvolveu o trabalho
        
### 12   DIFICULDADES ENCONTRADAS PELO GRUPO<br>
### 13   TRABALHO DE MINERAÇÃO DE DADOS
        a) captura das informaçõs
        b) integração com banco de dados em desenvolvimento
        c) atualização da documentação do trabalho incluindo a mineração de dados
        
### 13  FORMATACAO NO GIT: https://help.github.com/articles/basic-writing-and-formatting-syntax/

### 14 Backup completo do banco de dados postgres 
    a) deve ser realizado no formato "backup" 
        (Em Dump Options #1 Habilitar opções Don't Save Owner e Privilege)
    b) antes de postar o arquivo no git o mesmo deve ser testado/restaurado por outro grupo de alunos/dupla
    c) informar aqui o grupo de alunos/dupla que realizou o teste.
    
>## Marco de Entrega 04/Entrega Final em: (Data definida no cronograma)<br>
    
### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. Caso existam arquivos com conteúdos sigilosos, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário deste GIT, para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://sis4.com/brModelo/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")
