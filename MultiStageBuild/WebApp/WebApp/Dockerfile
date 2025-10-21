FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY WebApp.csproj ./
RUN dotnet restore

COPY . .
RUN dotnet publish "WebApp.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/runtime-deps:8.0-cbl-mariner2.0 as final
WORKDIR /app

COPY --from=build /app/publish .

# Expose port 80 to enable communication with the web app.
EXPOSE 80

ENTRYPOINT ["dotnet", "WebApp.dll"]
