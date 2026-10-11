# diagrama-dimensional-star-schema-
diagrama dimensional – star schema para aula primeiros passos com power bi
Modelagem Dimensional: Star Schema (Universidade)

Projeto de modelagem dimensional criado a partir de um diagrama relacional de uma universidade. O objetivo é analisar os dados dos professores: disciplinas ministradas, cursos e departamentos.

Diagrama

<img width="1173" height="714" alt="diagrama dimensional – star schema" src="https://github.com/user-attachments/assets/0a958227-3f78-493f-98bb-a748ab116e61" />


Objetivo

Transformar o modelo relacional (OLTP) em um esquema em estrela (OLAP), com foco em responder perguntas como:

Quantas disciplinas cada professor ministra por semestre?
Qual a carga horária ministrada por departamento?
Como a oferta de disciplinas evolui ao longo dos anos?
Granularidade da fato

1 linha = 1 professor ministrando 1 disciplina em 1 curso, em uma data de oferta.

Estrutura do modelo
Tabela fato

tabela_fato_professor_oferta

Tipo	Campos
Chaves estrangeiras	sk_professor, sk_departamento, sk_disciplina, sk_curso, sk_data_oferta_disciplina, sk_data_oferta_curso
Métricas	qtd_disciplinas, carga_horaria_ministrada, qtd_prerequisitos
Tabelas dimensão
Dimensão	Descrição
tabela_professor	Dados do professor: nome, regime de trabalho, data de admissão e se é coordenador
tabela_departamento	Nome, campus e professor coordenador
tabela_disciplina	Nome, carga horária, quantidade de pré-requisitos e semestre ideal
tabela_curso	Nome, nível e turno
tabela_data	Calendário: dia, mês, trimestre, semestre, ano e dia da semana
Decisões de modelagem
Alunos fora do escopo: as tabelas Aluno e Matriculado foram descartadas, pois o foco é o professor.
Relação N:N resolvida na fato: a tabela associativa Disciplina & Curso foi absorvida pelo grão da fato.
Pré-requisitos como atributo: as tabelas de pré-requisitos viraram o campo qtd_prerequisitos na dimensão disciplina, mantendo o modelo em estrela simples, sem snowflake.
Dimensão de datas com dois papéis (role-playing): a mesma tabela_data é usada para a data de oferta da disciplina e para a data de oferta do curso.
Chaves substitutas (sk_): cada dimensão tem uma chave própria, mantendo o id_ original como chave de negócio.
Campos assumidos: como o modelo relacional não tem dados de datas e alguns atributos descritivos, esses campos foram supostos, conforme permitido no enunciado do desafio.
Ferramentas
dbdiagram.io: criação do diagrama

Autor
Eric Nunes
