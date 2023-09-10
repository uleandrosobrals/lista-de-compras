#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/ListaDeCompas.API/ListaDeCompas.API.csproj", "src/ListaDeCompas.API/"]
RUN dotnet restore "src/ListaDeCompas.API/ListaDeCompas.API.csproj"
COPY . .
WORKDIR "/src/src/ListaDeCompas.API"
RUN dotnet build "ListaDeCompas.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ListaDeCompas.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ListaDeCompas.API.dll"]