# 1 - Repositorios Java:

	Git: 					http://143.125.232.199:8089/
	Maven:					http://143.125.232.199:5858
	SVN (Projetos não migrados para o GIT): http://143.125.232.2/repositorios/ProjetosJava
	SVN (Projetos antigos): 		http://143.125.232.2/repositorios/ProjetosJavaOld

# 2 - Configurar o Maven:

- Instalar o mvn

	$apt-get install maven

- Criar a pasta .m2 no home do usuario

- Copiar o arquivo mvn/settings-security.xml para a pasta .m2

- Rodar o comando abaixo com uma senha para o 'mvn' e copiar o valor com as { } para dentro do arquivo `settings-security.xml`

	$mvn  --encrypt-master-password <sua_senha>

- Copiar o arquivo mvn/settings.xml para a pasta .m2

- Rodar o comando abaixo e copiar o valor com as { } para os locais indicados dentro do arquivo `settings.xml`, alterar o usuário nos lugares indicados
		
	$mvn --encrypt-password <senha_usuario_do_maven>

- Para deploy segue o pom.xml de exemplo.

	    Para deploy inserir em seu pom.xml:
	    <distributionManagement>
		<repository>
		    <id>maven-criar-objects</id>
		    <name>maven-criar-objects</name>
		    <url>http://143.125.232.199:5858/repository/maven-criar-objects/</url>
		</repository>
	    </distributionManagement>

- Para projetos que utilizam o gradle colocar o arquivo mvn/init.gradle na pasta ~/.gradle (Configurar usuario e senha dentro do arquivo)
