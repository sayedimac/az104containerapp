#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["az104containerapp/az104containerapp.csproj", "az104containerapp/"]
RUN dotnet restore "az104containerapp/az104containerapp.csproj"
COPY . .
WORKDIR "/src/az104containerapp"
RUN dotnet build "az104containerapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "az104containerapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "az104containerapp.dll"]