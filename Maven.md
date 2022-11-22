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
<li>Instalar dependências: install, public um componente e disponibiliza no repositório local para reuso em outras aplicações</li>

```bash
C:\>projetos\mvn install
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

<h3><em>Repositórios</em></h3>
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

<h3><em>Como adicionar dependências ao projeto</em></h3>
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
<h3><em>Tipos de Dependência</em></h3>
<p>Existem dois tipos de dependências diretas e transitivas. As diretas são as declaradas no pom.xml e as transitivas são as dependências obrigatórias das dependências declaradas no pom.xml .</p>
<h3><em>Transitividade e Escopos</em></h3>
<p>Problemas de transitividade é buscar a referencia e inferir uma dependênicia quer queremos e acabar recebendo outras dependências que não iremos utilizar. </p>

<h4>Classpath</h4>
<li>Runtime: Tempo de execução </li>
<li>Test: Execução do teste</li>
<li>Compile: pra compilar a aplicação </li>

<p>É a referência que a aplicação tem para o momento de execução, e o Maven divide em 3 parte:</p>
<p>Para lidar com esses problemas, o Maven provê escopos para limitar a transitividade das dependências. Deve ser declarado dentro da tag dependency</p>.

```xml
<dependency>
	<scope>default</scope>
</dependency>
```

<p>Existem 6 tipos que podemos utilizar:</p>
<ol>
	<li>Escopo default: é uma dependência transitiva e está disponível em todos os classpaths </li>
	<li>Espoco provided: é uma dependência não transitiva e indica que será fornecida em tempo de execução por uma implementação na JDK ou via container. A dependência com esse escopo é adicionado no classpath <em>Compile</em> e no <em>Test</em> mas não em <em>Runtime</em>.</li>
	<li>Escopo runtime: indica que a dependência é necessária para execução e não para compilação. Maven inclui no classpath dos escopos de <em>Runtime</em> e <em>Test</em>.</li>
	<li>Escopo test: é uma dependência não transitiva e disponível somente para compilação e execução de testes.</li>
	<li>Escopo system: é uma dependência não transitiva. Similar ao escopo provided exceto por ser necessário prover o JAR explicitamente. A dependência com esse escopo é adicionado no classpath usado para <em>Compile</em> e no <em>Test</em> mas não em <em>Runtime</em>.</li>
	<li>Escopo import: Este escopo é disponível apenas com uma dependência do tipo pom e com tag 'dependencyManagement', permite importar dependências de outro projeto.</li>
</ol>

<h3><em>Dicas de escopos, dependências adicionais e exclusions</em></h3>
</h4>Dicas de escopos</h4>
<p>Como ver o classpath do meu projeto e ver como o Maven esta construindo cada escopo que existe na minha aplicação:</p>

```bash
C:\>projetos\mvn dependency:build-classpath -DincludeScope=compile
C:\>projetos\mvn dependency:build-classpath -DincludeScope=test
C:\>projetos\mvn dependency:build-classpath -DincludeScope=runtime
```

<h4>Dependências opcionais</h4>
<p>Utilizados quando uma dependência não é necessária para os projetos que irão reutilizar seu componente.</p>

```xml
<dependency>
	<optional>true</optional>
</dependency>

```
<h4>Exclusions</h4>
<p>Utilizado quando o componente que você usa, compartilha uma biblioteca que você já tem ou não quer ter disponível.</p>

```xml
<exclusions>
	<exclusion>
		<groupId>com.google.code.gson</groupId>
	</exclusion>
</exclusions>
```

<h2>Aula 5 - Maven Build Lifecycle</h2>
<h3><em>O que é?</em></h3>

<h4>Conceito de ciclo de vida de construção</h4>
	



<h4>Conceito e os comandos da ferramenta</h4>

<h4>Composto por 3 ciclos de vida</h4>

<h4>Cada ciclo de vida possui fases (Maven Phases)</h4>

<h4>Cada fase possui objetivos (Maven Goals)</h4>
<ol>
	<li>Default Lifecycle</li>
	Principal ciclo<br>
	Responsável pelo deploy local<br>
	Composto por 23 fases, sendo as principais:
		<ul>
			<li>validate</li>
			<li>compile</li>
			<li>test-compile</li>
			<li>test</li>
			<li>integration-test</li>
			<li>package</li>
			<li>install</li>
			<li>deploy</li>
		</ul>	
	<li>Clean Lifecycle</li>
	Ciclo intermediário<br>
	Responsável pela limpeza do projeto<br>
	Composto por 3 fases:
		<ul>
			<li>pre-clean</li>
			<li>clean</li>
			<li>post-clean</li>
		</ul>		
	<li>Site Lifecycle</li>
	Ciclo final<br>
	Responsável pela criação do site de documentação do projeto<br>
	Composto por 4 fases:
		<ul>
			<li>pre-site</li>
			<li>site</li>
			<li>post-site</li>
			<li>site-deploy</li>
		</ul>
</ol>

<p>São comandos, existem plugins para entregar a documentação, por exemplo, um projeto escrito em Java, vem com o javadoc, com a documentação toda pronta para entrega.</p>


<h2>Aula 6 - Multi-módulos</h2>

<h3><em>Projetos multi-módulos</em></h3>
<p>Vamos supor que uma equipe tem 4 projetos dividos em: core, service, webapp e controller, cada um com um repositório diferente. E esse time está trabalhando numa mesma feature, mas tendo que alterar todos esses projetos. </p>
<p>Pensando nisso surgiu a idéia de um projeto agregador com todos esse projetos internos, chamados de submódulos.</p>
<p>Para construir um multi-módulo vamos começar pelo terminal:</p>
<ol>

<li> Primeramente vamos criar o projeto agregador</li>

```bash
C:\projetos>mvn archetype:generate -DgroupId=one.digital.innovation -DartifactId=project-parent -Darchetype=maven-quick-start
```
<li> Abrir o projeto e fazer um alteração no pom.xml, incluir um packaging para indicar que é do tipo pom</li>

```xml
//

<groupId>one.digital.innovation</groupId>
<artifact>project-parent</artifact>
<version>1.0-SNAPSHOT</version>
<packaging>pom</packaging>

//
```

<li> Feito isso, voltamos ao terminal, entramos dentro do diretório do projeto e de lá executamos novamente o mesmo comando, só que agora como cada um dos nosso componentes:</li>

```bash
C:\projetos\project-parent>mvn archetype:generate -DgroupId=one.digital.innovation -DartifactId=core -Darchetype=maven-quick-start -DinteractiveMode=false

<<com
echo "enter"
com

C:\projetos\project-parent>mvn archetype:generate -DgroupId=one.digital.innovation -DartifactId=webapp -Darchetype=maven-quick-start -DinteractiveMode=false

<<com
echo "enter"
com

C:\projetos\project-parent>mvn archetype:generate -DgroupId=one.digital.innovation -DartifactId=service -Darchetype=maven-quick-start -DinteractiveMode=false

<<com
echo "enter"
com

C:\projetos\project-parent>mvn archetype:generate -DgroupId=one.digital.innovation -DartifactId=controller -Darchetype=maven-quick-start -DinteractiveMode=false
<<com
echo "enter"
com

```
<li> Abrir o projeto na IDE e verificar que o Maven adicionou os módulos dentro do projeto agregador.</li>

```xml
<modules>
	<module>core</module>
	<module>service</module>
	<module>controller</module>
	<module>webapp</module>
</modules>
```

<li> E cada módulo tem um parent, que é o "pai", no pom.xml</li>

```xml
<parent>
	<groupId>one.digital.innovation</groupId>
	<artifact>project-parent</artifact>
	<version>1.0-SNAPSHOT</version>
</parent>
```

</ol>

<h2>Aula 7 - Plugins</h2>
