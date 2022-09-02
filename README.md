<h1 align="center">Banco de dados para gerenciamento de uma faculdade</h1>


<h3 align="left"> 🎯 Objetivo do Banco de dados </h1> 
Realizar controles centralizados de alunos, professores, cursos, disciplinas, histórico escolar e turmas.

<h3 align="left"> ✅ Fases do projeto </h1> 

► Levantamento dos Requisitos 

► Identificação de Entidades Relacionamentos

► Modelo E-R

► Diagrama E-R

► Dicionário de Dados 

► Normalização

► Implementação

► Testes Básicos

<h1 align="center">🚀Começando </h1>

<h3 align="left"> 📌 Regras do Negocio </h1> 


- Um aluno só pode estar matriculado em um curso por vez
- Alunos possuem um codigo de identificação (RA)
- Cursos são compostos por disciplinas
- Cada Disciplina terá no máximo 30 alunos por turma
- As disciplinas podem ser obrigatórias ou optativas, depende do curso
- As disciplinas pertencem a departamentos específicos
- Cada disciplina possui um código de identificação
- Alunos podem trancar a matricula, não estando matriculados em nenhuma disciplina no semestre
- Em cada semestre cada aluno pode se matricular em no maximo 9 desciplinas
- O aluno só pode ser reprovado no máximo 3x na mesma disciplina
- A faculddade terá no maximo 3.000 alunos matriculados simultaneamente, em 10 cursos distintos
- Entram 300 alunos novos por ano
- Existem 90 disciplinas no total disponivel
- Um histórico Escolar traz todas as diciplinas cursadas por um aluno, incluindo nota final, frequência e período do curso realizado.
- Professores podem ser cadastrados mesmo sem lecionar disciplinas
- Existem 40 professores trabalhando na escola
- Cada professor irá lecionar no máximo 4 disciplinas diferentes
- Cada professor é vinculado a um departamento
- Professores são identificados por um código de professor


## 🔛 Identificando os Relacionamentos  

<h3 align="left"> ALUNO

- Aluno está matriculado em Curso
- Aluno Curso Disciplinas
- Aluno Realizou Disciplina

<h3 align="left"> PROFESSOR

- Professor Ministra Disciplina
- Professor Pertence a Departamento

<h3 align="left"> DEPARTAMENTO

- Departamento é Responsável por Disciplina
- Departamento Controla Curso

<h3 align="left"> DISCIPLINA

- Disciplina Depende de Disciplina
- Disciplina Pertence a curso

##  🔛 Identificando os Atributos 

<h3 align="left">Aluno

- RA
- Nome
- Sobrenome
- Endereço: Rua, Número, Bairro, CEP, Cidade, Estado
- Código do Curso
- Telefone

<h3 align="left"> Professor

- Código do Professor 
- Nome 
- Código do Departamento
- Status

<h3 align="left"> Disciplina

- Código da Disciplina
- Nome da Disciplina
- Descrição Curricular 
- Código de Departamento
- Número de Aluno

<h3 align="left"> Curso

- Código do Curso
- Nome do Curso
- Código do Deprtamento

<h3 align="left"> Departamento

- Código do Departamento
- Nome do Departamento

## 📐 Diagrama Entidade-Relacionamento - Modelo Conceitual

![Untitled](https://user-images.githubusercontent.com/112008347/188033574-5aae9800-f8be-4119-8c42-a6d800580bbe.png)

## Adicionando Atributos

![add atributos](https://user-images.githubusercontent.com/112008347/188033957-9e4d6ba4-2d12-450c-8ce0-a51338f21296.png)

## Calculando Cardinalidades

![Calculando Cardinalidades](https://user-images.githubusercontent.com/112008347/188034028-7108e28c-6c00-4dd3-92ec-b350645436fe.png)

## Eliminando Relacionamentos Muitos-para-Muitos

São relacionamento que certamente vão dar problemas mais para frente se tentar implementar no banco de dados, o relacionamento muitos para muitos deve ser desmembrado para não termos problemas com repetição ou integridade dos dados.

Por esta razão vamos criar entidades Associativas (1,N):

![Relacionamentos Muitos-para-Muitos](https://user-images.githubusercontent.com/112008347/188034116-fe7f2e0e-6038-4390-86ae-9ccd51275829.png)

![Relacionamentos Muitos-para-Muitos2](https://user-images.githubusercontent.com/112008347/188034159-2b463ecb-61c3-4bca-b4b9-ac97d64d881f.png)

## Entidade-Relacionamento - Modelo Lógico

![Entidade-Relacionamento - Modelo Lógico](https://user-images.githubusercontent.com/112008347/188034295-9eb808e7-d01a-4633-be42-3896cdd159d9.png)

## NORMALIZAÇÃO

<h3 align="left"> Primeira forma Normal

Uma tabela está na 1º forma normal quando:

- Existe uma Chave Primaria
- Somente possui valores atômicos
- Relação não possui atributos multivalorados ou relações aninhadas
- Relação não possui atributo composto

---

Na 1º Analise vamos precisar alterar as seguintes tabelas para ficar como a 1º forma normal

- Aluno: filiação(nome do pai e nome da mãe), contato e telefone
- Histórico: Período de realização (inicio e fim)

![1º Analise](https://user-images.githubusercontent.com/112008347/188034457-e30c9811-d5b7-442a-867d-ccc60591a692.png)

<h3 align="left"> Segunda forma Normal

Uma tabela está na 2º forma normal quando:

- Esta na 1º FN
- Todos atributos não-chave são funcionalmente dependentes de todas as partes da chave primaria
- Não existem dependências parciais, e atributos não dependem de chaves candidatas

Caso ao contrario, deve-se gerar uma nova tabela com os dados.

---

Na 2º Analise FN vamos precisar alterar as seguintes tabelas 

- Aluno: Nome_Rua; Num_Rua, CEP (não são dependentes da chave primaria que é o RA, podemos ter outro aluno morando na mesma rua) e Telefone
- Histórico: Período de realização (inicio e fim)

![2º Analise](https://user-images.githubusercontent.com/112008347/188034521-e2b887e1-aee6-4673-8673-5c39be494830.png)


<h3 align="left"> Terceira Forma Normal

Uma tabela está na 2º forma normal quando:

- Esta na 2º FN
- Não existirem dependências transitivas
- Se nenhuma coluna não-chave depender de outra coluna não chave
- Para cada atributo não chave que for um determinante na relação, crie uma nova tabela e esse atributo vai ser a PK na nova relação, precisamos mover todos os atributos que dependam dele para essa nova tabela e o atributo PK irá ficar como chave estrangeira para associar as relações entre as duas tabelas

---

Analisando não foi necessário fazer nenhuma alteração após avaliar a 3º forma Normal


