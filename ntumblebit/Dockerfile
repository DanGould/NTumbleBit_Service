FROM debian:jessie

# Add dotnet product feed
RUN apt-get update
RUN apt-get -y install curl libunwind8 gettext apt-transport-https

RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/dotnetdev.list'

# Install dotnet core SDK
RUN apt-get update
RUN apt-get -y install dotnet-sdk-2.0.0

# TODO run as NTumbleBit user
# Get NTumbleBit
COPY NTumbleBit /NTumbleBit/
WORKDIR /NTumbleBit
RUN dotnet restore

# TODO read config from shared volume
COPY server.config /.ntumblebit/Testnet/server.config

# Start the tumbler server
WORKDIR /NTumbleBit/NTumbleBit.ClassicTumbler.Server.CLI
RUN dotnet run -testnet
