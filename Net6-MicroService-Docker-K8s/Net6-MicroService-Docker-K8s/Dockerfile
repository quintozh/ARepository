#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Net6-MicroService-Docker-K8s/Net6-MicroService-Docker-K8s.csproj", "Net6-MicroService-Docker-K8s/"]
RUN dotnet restore "Net6-MicroService-Docker-K8s/Net6-MicroService-Docker-K8s.csproj"
COPY . .
WORKDIR "/src/Net6-MicroService-Docker-K8s"
RUN dotnet build "Net6-MicroService-Docker-K8s.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Net6-MicroService-Docker-K8s.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Net6-MicroService-Docker-K8s.dll"]