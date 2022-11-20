<h1>Gerenciamento de Dependências e Build em Java com Maven</h1>

<h2>Objetivos</h2>
- criar um projeto utilizando a ferramenta
- entender os principais conceitos 
- gerenciar dependencias do seu projeto
- configurar plugins e projetos com necessidades especifica

<h2>Aula 1 - Definição e instalação</h2>
<h3>O que é Apache Maven?</h3>
Ferramenta para gerenciar build e dependências de um projeto.
Primeira versão em julho de 2004, mantido pela Apache Software Foundation.
<h3>Qual problema ele resolve?</h3>
O Maven auxilar para enpacotar num formato específico, compilar os arquivos e realizar todos os testes.
<h3>O que é Maven?</h3>
Endereça como o software foi construído e suas dependências através do POM(Project Object Model).
Facilita a compreensão do desenvolvedor.
Fornecer informações de qualidade.

## Aula 2 - Primeiro projeto e conceitos
<h3>Criando um projeto via linha de comando</h3>
Abra o bash na pasta de projeto e digite o seguinte comando:

```bash
C:\>projetos\mvn archetype:generate -DgroupID=one.digitalinnovation -DartifactId=quick-start-maven -Darchetype=maven-archetype-quickstart -DinteractiveMode=false
```

Sendo:

<li>groupId: nome do pacote</li>
<li>artifact: nome do projeto</li>
<li>archetype: são arquetipos de templates Java</li>

<h3>Principais comandos</h3>

<li>Compilar: compile, todos os arquivos são e adicionados no recente criado diretório 'target'</li>

```bash
C:\>projetos\mvn compile
```
<li>Testar: test, efetua os teste da aplicação</li>

```bash
C:\>projetos\mvn test
```
<li>Empacotar: package, criar o jar da aplicação</li>

```bash
C:\>projetos\mvn package
```
<li>Limpar diretório de trabalho: clean, apaga o diretório 'target'</li>

```bash
C:\>projetos\mvn clean
```
<h3>Criando diferente tipos de projeto</h3>

<h4>Como?</h4>
<p>Através do Maven archetype, nada mas é do que um template que possibilita a personalização e configuração de como um projeto vai ser construído, definimos versão de componentes, quais componentes vão ser adicionados automaticamente, organização de pacote e organização de arquivos.</p>
<p>Pesquisar por "maven archetype list", para ver qual o template melhor supre a necessidade do projeto.</p>

## Aula 3 - POM, Dependência e Repositórios
## Aula 4 - Gerenciamento de Dependencia
## Aula 5 - Maven Build Lifecycle
## Aula 6 - Multi-módulos
## Aula 7 - Plugins
