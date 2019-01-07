FROM java:8-jre
LABEL author Denis Luchkin-Zhou <wyvernzora@gmail.com>

# Update container
RUN apt-get update && \
    apt-get upgrade --yes --force-yes && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set up working directory
WORKDIR /minecraft

# Create minecraft user, download server files and accept EULA
USER root
RUN useradd -m -U minecraft && \
    mkdir -p /minecraft/world && \
    wget https://media.forgecdn.net/files/2646/580/Enigmatica2Server-1.54.zip && \
    unzip Enigmatica2Server-1.54.zip && \
    rm Enigmatica2Server-1.54.zip && \
    echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
	echo "$(date)" >> eula.txt && \
	echo "eula=TRUE" >> eula.txt && \
	chown -R minecraft:minecraft /minecraft

# Start the server
USER minecraft
EXPOSE 25565
VOLUME ["/minecraft/world", "/minecraft/logs", "/minecraft/backups"]
CMD ["/bin/bash", "/minecraft/ServerStartLinux.sh"]
