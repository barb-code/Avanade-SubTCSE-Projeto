#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AvanadeSubTCSE.Projeto.Api/AvanadeSubTCSE.Projeto.Api.csproj", "AvanadeSubTCSE.Projeto.Api/"]
RUN dotnet restore "AvanadeSubTCSE.Projeto.Api/AvanadeSubTCSE.Projeto.Api.csproj"
COPY . .
WORKDIR "/src/AvanadeSubTCSE.Projeto.Api"
RUN dotnet build "AvanadeSubTCSE.Projeto.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AvanadeSubTCSE.Projeto.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AvanadeSubTCSE.Projeto.Api.dll"]