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
    wget https://media.forgecdn.net/files/2642/264/StoneBlock-1.0.31-Server.zip && \
    unzip StoneBlock-1.0.31-Server.zip && \
    rm StoneBlock-1.0.31-Server.zip && \
    echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
	echo "$(date)" >> eula.txt && \
	echo "eula=TRUE" >> eula.txt && \
    /bin/bash /minecraft/Install.sh && \
	chown -R minecraft:minecraft /minecraft

# Start the server
USER minecraft
EXPOSE 25565
VOLUME ["/minecraft/world"]
CMD ["/bin/bash", "/minecraft/LaunchServer.sh"]
