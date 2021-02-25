#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /wapp

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["DockerTest.csproj", "WebApp/"]
RUN dotnet restore "WebApp/DockerTest.csproj"
COPY . .

RUN dotnet build "DockerTest.csproj" -c Release -o /wapp/build

FROM build AS publish
RUN dotnet publish "DockerTest.csproj" -c Release -o /wapp/publish

FROM base AS final
WORKDIR /wapp
COPY --from=publish /wapp/publish .

ENV ASPNETCORE_URLS http://+:5012
EXPOSE 5012

ENTRYPOINT ["dotnet", "DockerTest.dll"]