FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY DockerExample/DockerExample.csproj DockerExample/
RUN dotnet restore DockerExample/DockerExample.csproj
COPY . .
WORKDIR /src/DockerExample
RUN dotnet build DockerExample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerExample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerExample.dll"]
