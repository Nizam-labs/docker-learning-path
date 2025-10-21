FROM mcr.microsoft.com/dotnet/sdk:8.0
COPY DockerConsole/ ./docker-size-test
WORKDIR /docker-size-test/
RUN dotnet build -c Release
ENTRYPOINT ["dotnet", "run", "-c", "Release", "--no-build"]