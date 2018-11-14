#Tutorial de instalação e configuração do debian

#1 - Criação da pendrive

	Modo FORDUMMIES:
		Abra o Disks
		Formate a pen-drive para "Sem partição"
		Clique em opções (engrenagem ou listras) no topo direito
		Selecione para restaurar uma imagem 
		Selecione a ISO do sistema

	Modo 1 (Com grafico): 
		$apt-get install pv dialog
		$dd if=/path/to/linux.iso | pv | dd of=/dev/sdX bs=4M && sync

	Modo 2:
		Com a pendrive sem partição
		$dd if=/path/to/linux.iso of=/dev/sdX bs=4M && sync

#2 - Instalação

	Instalar sem swap

    Para desativar o swap:

        $cp /etc/fstab /etc/fstab_backup
        $nano /etc/fstab

#3 - Atualização

	* Nunca fazer nada no computador enquanto está atualizando
	* Reiniciar o computador ao fim do upgrade

        $apt-get update
        $apt-get upgrade -y 
	
#4 - Firmwares

        $apt-get install firmware-atheros firmware-linux firmware-linux-free firmware-linux-nonfree firmware-misc-nonfree firmware-realtek 

#5 - Padronização do sistema
	
	Crie uma pasta /sdk
	Crie um link simbolico para o java em /sdk/jdk
	Crie uma pasta /sdk/repositorios
	Dentro da pasta os projetos devem ser mapeados exatamente igual ao repositorio. Exemplo:
		Projeto 'Servidor eTeorika': http://{link_repositorio}/java/eteorika/server-eteorika.git
		Pasta: /sdk/repositorios/java/eteorika/server-eteorika

#6 - Configuração de PROFILE

	*** INSIRA NO FINAL DO ARQUIVO ***

	$gedit /etc/profile

		#CONFIGURACAO DE PROXY DO TERMINAL	
		export https_proxy=http://username:password@143.125.232.1:8080
		export http_proxy=http://username:password@143.125.232.1:8080
		export ftp_proxy=http://username:password@143.125.232.1:8080

		#JAVA
		export JAVA_HOME=/sdk/jdk
		export CLASSPATH="$JAVA_HOME/lib"
		export PATH="$JAVA_HOME/bin":"$PATH"
		export MANPATH=/usr/local/man:/usr/man:"$JAVA_HOME/man"

		#GRADLE
		export GRADLE_HOME=/sdk/gradle
		export PATH="$PATH":"$GRADLE_HOME/bin"

#7 - Configurar o java como padrão
	
		$sudo update-alternatives --install "/usr/bin/java" "java" "/sdk/jdk/bin/java" 1
		$sudo update-alternatives --install "/usr/bin/javac" "javac" "/sdk/jdk/bin/javac" 1
		$sudo update-alternatives --config java
		$sudo update-alternatives --config javac

#8 - Configurar o java para navegador
	
		cd /usr/lib/mozilla/plugins/
		ln -s /sdk/jdk/jre/lib/amd64/libnpjp2.so


#9 - Otimização do sistema

	Melhor para instalar pacotes pelo terminal:
		$apt-get install gdebi

	Editar o menu principal
		$apt-get install menulibre	

	Auto completar
		$apt-get install bash-completion

	Otimizações
		$apt-get install preload
		$apt-get install ulatency

	TODOS
		$apt-get install gdebi menulibre bash-completion preload ulatency

	TMP na RAM:
	
		abra o seu terminal e cole o comando abaixo para abrir o arquivo fstab

			sudo gedit /etc/fstab

		No arquivo que se abrir adicione as seguintes linhas no final:

		# Move /tmp to RAM
		tmpfs /tmp tmpfs defaults,noexec,nosuid 0 0

#10 - Instalação do Workbench

	$apt-get install mysql-workbench mysql-workbench-data 
	
	Em caso de: Failed to load module “canberra-gtk-module” … but already installed

		apt install libcanberra-gtk-module libcanberra-gtk3-module
		apt update ; apt purge mysql-workbench mysql-workbench-data
		apt install mysql-workbench mysql-workbench-data 

#11 - Configuração do Sudo

	$echo "seususuario ALL=(ALL:ALL) ALL" >> /etc/sudoers

#12 - Configuração de WIFI para roteadores antigos (Lista wifi mas não conecta)

	$nano /etc/NetworkManager/NetworkManager.conf

		[device]
		wifi.scan-rand-mac-address=no

	$systemctl restart NetworkManager 

#13 - Netbeans performance tunning (8GB RAM)

	Abrir o arquivo de configuração
		
		$NB_HOME/etc/netbeans.conf

	Opções

		-J-Xms2048m   --> Memoria reservada incialmente
		-J-Xmx4096m   --> Memoria maxima permitida

		-Dsun.java2d.opengl=true	--> Gerenciamento de UI via OpenGL
		-Dsun.java2d.d3d=false		--> Desativa o recurso de Direct3D
		-Dswing.aatext=true		--> Font anti-aliasing
	
#14 - Corrigindo a exibição de videos no opera

		fonte: https://www.vivaolinux.com.br/dica/Reproducao-de-videos-do-Facebook-ffmpeg-no-Opera-em-Deepin-155-Resolvido

	Como root, vá até a pasta que o Opera está instalado: /usr/lib/x86_64-linux-gnu/opera 

	Cole o arquivo desta pagina libffmpeg.so o substituindo

#15 - Android Studio no Linux 64:

	$sudo apt-get install libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1




