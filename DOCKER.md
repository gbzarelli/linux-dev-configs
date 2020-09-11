# Create GITLAB:
	docker run --detach \
	    --hostname 'localhost' \
	    --restart=always
	    --name helpdev_gitlab \
	    --publish 8089:80 \
	    --volume /opt/repositories/gitlab/config:/etc/gitlab \
	    --volume /opt/repositories/gitlab/logs:/var/log/gitlab \
	    --volume /opt/repositories/gitlab/data:/var/opt/gitlab \
	    gitlab/gitlab-ce

	    Documentação:
			https://hub.docker.com/r/gitlab/gitlab-ce/
			https://docs.gitlab.com/omnibus/docker/

# Configurar acesso externo:
	Editar: /opt/repositories/gitlab/config/gitlab.rb
	Descomentar external_url e inserir a url (lembrar de colocar 'http://{nome_ou_ip}')

# Gitlab - Backup and Restore
	https://docs.gitlab.com/ee/raketasks/backup_restore.html
		docker exec -it <container name> gitlab-rake gitlab:backup:create
		docker exec -it <container name> gitlab-rake gitlab:backup:restore
		( Dir backup: <dir data>/backups )
		Obs: Restaure o backup sempre na mesma versão do gitlab.

	Para inserir na CRON: (EXECUÇÃO AS 18:30, todos os dias)
		30 18   * * *   root    docker exec helpdev_gitlab gitlab-rake gitlab:backup:create CRON=1

# Upgrade GitLab:
	1 - Esteja com o ambiente todo configurado. E rodando.
	2 - Faça um backup para segurança
	3 - docker stop helpdev_gitlab : docker rm helpdev_gitlab
	4 - Execute o comando para criar o docker. Assim ele pega a ultima versão e mantem os diretorios.


# Nexus3 - Repositorio Maven
	docker run -d -p 5858:8081 --restart=always --name nexus -v /opt/nexus-data:/nexus-data sonatype/nexus3
	Caso tenha backup:
		chown 200 -R /opt/nexus-data

####! UTILS !####

# Comandos uteis
	docker ps -a
	docker logs <container name>
	docker rm <container name>
	docker rmi <image_name>
	docker exec -it <container name> bash

# Sample create a debian image:
	docker pull debian
	docker run -it --name dockerName debian
	docker start dockerName
	docker attach dockerName OR docker exec -it dockerName bash


    Build context example

    Create a directory for the build context and cd into it. Write “hello” into a text file named hello and create a Dockerfile that runs cat on it. Build the image from within the build context (.):

    mkdir myproject && cd myproject
    echo "hello" > hello
    echo -e "FROM busybox\nCOPY /hello /\nRUN cat /hello" > Dockerfile
    docker build -t helloapp:v1 .

    Move Dockerfile and hello into separate directories and build a second version of the image (without relying on cache from the last build). Use -f to point to the Dockerfile and specify the directory of the build context:

    mkdir -p dockerfiles context
    mv Dockerfile dockerfiles && mv hello context
    docker build --no-cache -t helloapp:v2 -f dockerfiles/Dockerfile context
