<h1>Gerenciamento de Dependências e Build em Java com Maven</h1>

<h2>Objetivos</h2>
<li>Criar um projeto utilizando a ferramenta</li>
<li>Entender os principais conceitos</li>
<li>Gerenciar dependências do seu projeto</li>
<li>Configurar plugins e projetos com necessidades específicas</li>

<h2>Aula 1 - Definição e instalação</h2>
<h3><em>O que é Apache Maven?</em></h3>
Ferramenta para gerenciar build e dependências de um projeto.
Primeira versão em julho de 2004, mantido pela Apache Software Foundation.
<h3><em>Qual problema ele resolve?</em></h3>
O Maven auxilar para enpacotar num formato específico, compilar os arquivos e realizar todos os testes.
<h3><em>O que é Maven?</em></h3>
Endereça como o software foi construído e suas dependências através do POM(Project Object Model).
Facilita a compreensão do desenvolvedor.
Fornecer informações de qualidade.

## Aula 2 - Primeiro projeto e conceitos
<h3><em>Criando um projeto via linha de comando</em></h3>
Abra o bash na pasta de projeto e digite o seguinte comando:

```bash
C:\>projetos\mvn archetype:generate -DgroupID=one.digitalinnovation -DartifactId=quick-start-maven -Darchetype=maven-archetype-quickstart -DinteractiveMode=false
```

Sendo:

<li>groupId: nome do pacote</li>
<li>artifact: nome do projeto</li>
<li>archetype: são templates para projetos Java</li>

<h3><em>Principais comandos</em></h3>

<li>Compilar: compile, todos os arquivos são compilados e adicionados no recente criado diretório 'target'</li>

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
<h3><em>Criando diferente tipos de projeto</em></h3>

<h4>Como?</h4>
<p>Através do Maven archetype, nada mas é do que um template que possibilita a personalização e configuração de como um projeto vai ser construído, definimos versão de componentes, quais componentes vão ser adicionados automaticamente, organização de pacote e organização de arquivos.</p>
<p>Pesquisar por "maven archetype list", para ver qual o template melhor supre a necessidade do projeto.</p>

<h2>Aula 3 - POM, Dependência e Repositórios</h2>
<h3><em>POM</em></h3>
<li>POM - Project Object Model</li>
<li>Unidade fundamental de trabalho</li>
<li>Tem formato XML</li>
<li>Detalha o projeto</li>
<li>Detalha como construir o projeto</li>
<li>Maven sempre procura pelo pom.xml para realizar sua execução</li>

<h4>Mais detalhes pom.xml</h4>
<li>Nome do projeto</li>
<li>Dependências</li>
<li>módulos</li>
<li>configuração de build</li>
<li>Detalhes do projeto(nome, descrição, licença, url)</li>
<li>Configuração de ambiente(repositório, tracking, profiles)</li>

<h4>Pom.xml básico</h4>

```xml
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.mycompany.app</groupId>
	<artifact>my-app</artifact>
	<version>1</version>
</project>
```

<p>O maven trabalha com conceito de herança, por exemplo se voce passar o pom com apenas essas configurações ele vai extender de um superPOM as configurações que necessita.</p>

<h3>Repositórios</h3>
<p>São locais onde podemso encontrar plugins e bibliotecas que o Maven provê. Há dois tipos: o local e o remoto.</p>
<li>Repositório Remoto</li>
<p>É o local central utilizado pelo Maven para buscar os artefatos. Configurado automaticamente pelo super POM para utilizar o Maven Central</p> 

<p>Trecho do super POM</p>

```xml
<repositories>
	<repository>
		<id>central</id>
		<name>Central Repository</name>
		<url>http://repo.maven.apache.org/maven2</url>
		<layout>default</layout>
		<snapshot>
			<enabled>false</enabled>
		</snapshot>
	</repository>
</repositories>
```

<p>Configuração de repositório de plugin</p>

```xml
<pluginRepositories>
	<pluginRepository>
		<id>central</id>
		<name>Central Repository</name>
		<url>http://repo.maven.apache.org/maven2</url>
		<layout>default</layout>
		<snapshot>
			<enabled>false</enabled>
		</snapshot>
		<releases>
			<updatePolicy>never</updatePolicy>
		</releases>
	</pluginRepository>
</pluginRepositories>
```
<p>Essas são as configurações padrão.</p>
<li>Repositório Local</li>
<p>É o repositório na máquina utilizado pelo Maven para buscar os artefatos. Estratégia de caching. Ficam localizados no diretório ".m2\repository".</p>

<li>Fonte de consulta</li>

 - maven.apache.org/guides/introdution/introdution-to-repositories.html
 - super-pom.html
 - repo.maven.apache.org/maven2
 - mvnrepository.com

<h3>Como adicionar dependências ao projeto</h3>
<p>Basta ir ao pom.xml e localizar a tag dependecies e adicionar o groupId, o artifactId e o version</p>

```xml
<dependecies>
	<dependecy>
		<groupId>one.digitalinnovation</groupId>
		<artifactId>app-spring</artifactId>
		<version>1.0.0</version>
	</dependecy>
</dependecies>
```

<h4>Propriedades</h4>
<li>groupId: é como se fosse o id da organização. Segue as regras de nomes de pacote Java</li>
<li>artifactId: nome do projeto em si</li>
<li>version: número da versão que será utilizada</li>
<p>Adicione a dependência no pom.xml, após ir no terminal e digital o comando 'mvn compile' para baixar a dependência adicionada.</p>



<h2>Aula 4 - Gerenciamento de Dependencia</h2>

<h2>Aula 5 - Maven Build Lifecycle</h2>

<h2>Aula 6 - Multi-módulos</h2>

<h2>Aula 7 - Plugins</h2>
