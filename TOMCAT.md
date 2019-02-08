# Configurar tomcat 9
## Configurar arquivos de usuarios:

	$emacs conf/tomcat-users.xml

	Adicionar usuario com permissão total:
  
  ``` xml
    <role rolename="tomcat"/>
    <user username="tomcat" password="myPass" roles="tomcat,standard,manager-gui,manager-status,manager-script,manager-jmx,admin-gui,admin-script"/>
  ```
## Editar conf/server.xml para liberar https

  ``` xml
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
               maxThreads="150" SSLEnabled="true">
        <SSLHostConfig>
            <Certificate 
            	certificateKeystoreFile="conf/cert/helpdev.jks"
                type="RSA" 
			/>
        </SSLHostConfig>
    </Connector> 
  ```
## Editar o arquivo 'webapps/{aplicacao}/META-INF/context.xml' para restrições de acesso
-- Editar em - webapps/manager - webapps/host-manager - webapps/ROOT - Para restrição da home
  ``` xml
		allow="200\.100\.101\.102|200\.100\.101\.103|200\.100\.101\.104"
  ```
  Obs. As pastas que não tiver o META-INF (no caso da ROOT), basta criar no mesmo padrão. (cp -R webapps/manager/META-INF webapps/ROOT)
