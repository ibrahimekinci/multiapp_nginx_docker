#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /wapi

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["DockerTest.csproj", "WebApi/"]
RUN dotnet restore "WebApi/DockerTest.csproj"
COPY . .

RUN dotnet build "DockerTest.csproj" -c Release -o /wapi/build

FROM build AS publish
RUN dotnet publish "DockerTest.csproj" -c Release -o /wapi/publish

FROM base AS final
WORKDIR /wapi
COPY --from=publish /wapi/publish .

ENV ASPNETCORE_URLS http://+:5013
EXPOSE 5013

ENTRYPOINT ["dotnet", "DockerTest.dll"]