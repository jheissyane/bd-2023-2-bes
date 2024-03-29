## Resultado

Clique [AQUI](../media/bd-2023-2-bes-resumo.pdf) para ver as notas.

#### Avaliação em 05/10/2023
1. Conforme enunciado da questão, a definição de banco de dados ser tal que "englobe o conteúdo das seis definições apresentadas". Nesse sentido, a definição deve mencionar: (1) conjunto de dados; (2) dados relacionados entre si; (3) dados operacionais (reflete a dinâmica de algum domínio); (4) dados armazenados (os dados são retidos/guardados, pois possuem valor); (5) dados usados (há audiência, o que inclui o uso de sistemas/aplicações).
2. Apresentar exemplos de metadados, em vez de classificação de metadados. Os exemplos devem ser contextualizados, evitando respostas curtas que dão margem a abstração e ambiguidade (dado ou metadado?). Por exemplo: 'título de um livro', em vez de 'título'.

#### Avaliação em 19/10/2023
- Sobre definição, construção, manipulação e compartilhamento de banco de dados -> a construção denota a armazenagem de dados em meio controlado pelo SGBD.
- Quantas cópias do livro intitulado “Tribo Perdida” existem na unidade da biblioteca cujo nome é “Central”? -> LIVRO; LIVRO_COPIAS; UNIDADE_BIBLIOTECA.
- Recupere o nome de todos os usuários que não possuem livros emprestados em seu nome. -> LIVROS_EMPRESTIMOS; USUARIO
- Para cada livro que é emprestado da unidade da biblioteca cujo nome é “Central” e cuja data de devolução é hoje, recupere o título do livro, o nome e o endereço do usuário que pegou o livro emprestado.	-> LIVRO; LIVROS_EMPRESTIMOS; UNIDADE_BIBLIOTECA; USUARIO
- Para cada unidade da biblioteca, recupere o nome da unidade e o número total de livros emprestados pela unidade.	-> LIVROS_EMPRESTIMOS; UNIDADE_BIBLIOTECA
- Recupere o nome, endereço e número de livros emprestados para todos os usuários que possuem mais de cinco livros emprestados.	-> LIVROS_EMPRESTIMOS; USUARIO
- Para livro cujo autor (ou coautor) é “Stephen King”, recupere o título e o número de cópias pertencentes à unidade da biblioteca cujo nome é “Central”.	-> LIVRO; LIVRO_AUTOR; LIVRO_COPIAS; UNIDADE_BIBLIOTECA

#### Avaliação em 26/10/2023

1. RESULT ← π <sub>Pnome</sub> ( FUNCIONARIO ⋈ <sub>Cpf = Fcpf</sub> DEPENDENTE )
1. AUX ← π <sub>Cpf_gerente</sub> ( FUNCIONARIO ⋈ <sub>Cpf_supervisor = Cpf_gerente</sub> DEPARTAMENTO )<br>RESULT ← π<sub>Pnome</sub> ( FUNCIONARIO ⋈ <sub>Cpf = Cpf_gerente</sub> AUX )
1. RESULT ← π <sub>T1.Fcpf</sub> ( ρ <sub>T1</sub> (TRABALHA_EM) ⋈ <sub>T1.Fcpf = T2.Fcpf</sub> &#8743; <sub>T1.Pnr &#8800; T2.Pnr</sub> ρ <sub>T2</sub> (TRABALHA_EM) )

#### Avaliação em 09/11/2023

1. PRODUTO_CENTRAL ← π <sub>Produto</sub> ( σ <sub>Unidade="Central"</sub> ( FABRICA ) )<br>
RESULT ← π <sub>Cliente</sub> ( PRODUTO_CENTRAL ⋈ <sub>PRODUTO_CENTRAL.Produto = USA.Produto</sub> USA )
1. PRODUTO_CENTRAL ← π <sub>Produto</sub> ( σ <sub>Unidade="Central"</sub> ( FABRICA ) )<br>
CLIENTE_CENTRAL ← π <sub>Cliente</sub> ( PRODUTO_CENTRAL ⋈ <sub>PRODUTO_CENTRAL.Produto = USA.Produto</sub> USA )<br>
RESULT ← π <sub>Cliente</sub> ( USA )  &#8213; CLIENTE_CENTRAL
1. PRODUTO_CENTRAL ← π <sub>Produto</sub> ( σ <sub>Unidade="Central"</sub> ( FABRICA ) )<br>
PRODUTO_NAO_CENTRAL ← π <sub>Produto</sub> ( FABRICA ) &#8213; PRODUTO_CENTRAL<br>
CLIENTE_NAO_CENTRAL ← π <sub>Cliente</sub> ( PRODUTO_NAO_CENTRAL ⋈ <sub>PRODUTO_NAO_CENTRAL.Produto = USA.Produto</sub> USA )<br>
RESULT ← π <sub>Cliente</sub> ( USA )  &#8213; CLIENTE_NAO_CENTRAL

#### Avaliação em 16/11/2023

1. SELECT Pnome<br>FROM FUNCIONARIO JOIN DEPENDENTE<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf
2. SELECT Pnome<br>FROM FUNCIONARIO JOIN TRABALHA_EM<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf
3. SELECT PNOME<br>FROM FUNCIONARIO JOIN<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;( TRABALHA_EM AS T1 JOIN TRABALHA_EM AS T2<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON T1.Fcpf = T2.Fcpf AND T1.Pnr != T2.Pnr )<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON FUNCIONARIO.Cpf = T1.Fcpf

#### Avaliação em 23/11/2023

1. SELECT Pnome, Unome, Nome_dependente<br>FROM FUNCIONARIO LEFT OUTER JOIN DEPENDENTE<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf
1. SELECT Pnome, Unome, Nome_dependente<br>FROM FUNCIONARIO JOIN DEPENDENTE<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON Cpf = Fcpf<br>WHERE ( Nome_dependente LIKE "FE%" OR Pnome LIKE "FE%")<br>AND&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;( Nome_dependente LIKE "%DO" OR Pnome LIKE "%DO")

#### Avaliação em 30/11/2023

1. SELECT P.CodProd, P.Nome, SUM(VI.QtdeVenda), SUM(VI.QtdeVenda * P.Preco)<br>
FROM PRODUTO AS P<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN VENDA_ITEM AS VI ON P.CodProd = VI.CodProd<br>
GROUP BY P.CodProd, P.Nome
1. SELECT P.CodProd, P.Nome<br>
FROM PRODUTO AS P<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN VENDA_ITEM AS VI ON P.CodProd = VI.CodProd<br>
GROUP BY P.CodProd, P.Nome<br>
HAVING SUM(VI.QtdeVenda * P.Preco) > 10000
1. SELECT C.CPF, C.Nome, SUM(VI.QtdeVenda), SUM(VI.QtdeVenda * P.Preco)<br>
FROM CLIENTE AS C<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN VENDA AS V	ON C.CPF = V.CPF<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN VENDA_ITEM AS VI ON V.NumNF = VI.NumNF<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;JOIN PRODUTO AS P ON VI.CodProd = P.CodProd<br>
GROUP BY C.CPF, C.Nome

#### Avaliação em 07/12/2023

_Script_ do banco de dados:<br>
CREATE TABLE VENDE ( Bar varchar(30), Cerveja varchar(30));<br>
INSERT INTO VENDE VALUES ('Pipoca', 'Skol');<br>
INSERT INTO VENDE VALUES ('Pipoca', 'Brahma');<br>
INSERT INTO VENDE VALUES ('Pipoca', 'Antarctica');<br>
INSERT INTO VENDE VALUES ('Pipoca', 'Spaten');<br>
INSERT INTO VENDE VALUES ('Pipoca', 'Heineken');<br>
INSERT INTO VENDE VALUES ('Alvorada', 'Skol');<br>
INSERT INTO VENDE VALUES ('Alvorada', 'Bohemia');<br>
INSERT INTO VENDE VALUES ('Alvorada', 'Brahma');<br>
INSERT INTO VENDE VALUES ('Chapada', 'Amstel');<br>
INSERT INTO VENDE VALUES ('Chapada', 'Erdinger');<br>
CREATE TABLE GOSTA ( Pessoa varchar(30), Cerveja varchar(30));<br>
INSERT INTO GOSTA VALUES ('Lia', 'Skol');<br>
INSERT INTO GOSTA VALUES ('Lia', 'Bohemia');<br>
INSERT INTO GOSTA VALUES ('Maria', 'Erdinger');<br>
INSERT INTO GOSTA VALUES ('Maria', 'Amstel');<br>
INSERT INTO GOSTA VALUES ('Pedro', 'Antarctica');<br>
INSERT INTO GOSTA VALUES ('Pedro', 'Spaten');<br>
INSERT INTO GOSTA VALUES ('Pedro', 'Brahma');<br>
INSERT INTO GOSTA VALUES ('Ricardo', 'Heineken');

1. SELECT DISTINCT Pessoa FROM GOSTA<br>
WHERE Cerveja IN (<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT Cerveja FROM VENDE WHERE Bar = 'Pipoca'<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EXCEPT<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT Cerveja FROM VENDE WHERE Bar != 'Pipoca' )
1. SELECT Pessoa FROM GOSTA<br>
EXCEPT<br>
SELECT Pessoa<br>
FROM GOSTA NATURAL JOIN VENDE<br>
WHERE Bar = 'Pipoca'
1. SELECT DISTINCT Pessoa FROM GOSTA<br>
EXCEPT<br>
SELECT Pessoa FROM GOSTA WHERE Cerveja NOT IN (<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT Cerveja FROM VENDE WHERE Bar = 'Pipoca' )

#### Avaliação em 14/12/2023

1. SELECT DISTINCT X.NOME FROM PACIENTE V JOIN MEDICO W JOIN MEDICAMENTO X JOIN CONSULTA Y JOIN PRESCRICAO Z ON V.CPF = Y.CPF AND W.CRM = Y.CRM AND Z.CPF = Y.CPF AND Z.DATAHORA = Y.DATAHORA AND Z.CODIGO = X.CODIGO WHERE V.NOME = W.NOME GROUP BY Y.CPF, Y.CRM, X.CODIGO, X.NOMEHAVING COUNT(*) > 1
1. Pode ter valores repetidos nas tuplas de QUESTAO. Pode ter valor nulo em algumas das tuplas de QUESTAO. 
1. A ordenação das tuplas de uma relação é indiferente, visto que uma relação é definida como um conjunto de tuplas. Uma tupla é uma lista ordenada de valores, então há uma posição relativa pré-definida para cada valor de atributo na tupla (por exemplo, o valor “13/02/2000”, pertinente ao atributo “data de nascimento”, é o terceiro valor na lista de valores de uma tupla).

#### Avaliação em 18/01/2024

As respostas podem ser obtidas na prova corrigida.

#### Avaliação em 25/01/2024

ALUNO (Matricula, Nome, DataIngr)<br>
ALUNO (Matricula) IS PRIMARY KEY<br>
DISCIPLINA (Codigo, Descricao, Ementa)<br>
DISCIPLINA (Codigo) IS PRIMARY KEY<br>
CURSO (Numero, Nome, Diretor, Creditos)<br>
CURSO (Numero) IS PRIMARY KEY<br>
PROFESSOR (Matricula, Nome, NumCurso)<br>
PROFESSOR (Matricula) IS PRIMARY KEY<br>
PROFESSOR (NumCurso) REFERENCES CURSO (Numero)<br>
TURMA (CodDisc, CodTurma, Semestre, Sala, Horario, MatProf)<br>
TURMA (CodDisc, CodTurma, Semestre) IS PRIMARY KEY<br>
TURMA (CodDisc) REFERENCES DISCIPLINA (Codigo)<br>
TURMA (MatProf) REFERENCES PROFESSOR (Matricula)<br>
MATRICULA (MatAluno, CodDisc, CodTurma, Semestre)<br>
MATRICULA (MatAluno, CodDisc, CodTurma, Semestre) IS PRIMARY KEY<br>
MATRICULA (MatAluno) REFERENCES ALUNO (Matricula)<br>
MATRICULA (CodDisc, CodTurma, Semestre) REFERENCES TURMA (CodDisc, CodTurma, Semestre)<br>
NOTA (MatAluno, CodDisc, CodTurma, Semestre, Seq, Nota)<br>
NOTA (MatAluno, CodDisc, CodTurma, Semestre, Seq) IS PRIMARY KEY<br>
NOTA (MatAluno, CodDisc, CodTurma, Semestre) REFERENCES MATRICULA (MatAluno, CodDisc, CodTurma, Semestre)

