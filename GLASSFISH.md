# GLASSFISH - VERSÕES
	- Glassfish 5.0.1 -> https://download.oracle.com/glassfish/5.0.1/nightly
	- Java -> jdk1.8.0_181

# MUDAR SENHA
	./glassfish/bin/asadmin change-admin-password
		Obs: Usuario default: admin / Senha default: {sem senha}

# HABILITAR ADMIN REMOTO (Secure Admin must be enabled to access the DAS remotely)
	./glassfish/bin/asadmin enable-secure-admin

# INICAR E PARAR SERVIÇO:
	./glassfish/bin/asadmin stop-domain
	./glassfish/bin/asadmin start-domain
