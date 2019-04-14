FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["NetCoreApp.csproj", ""]
RUN dotnet restore
COPY . .
WORKDIR "/src/"
RUN dotnet build "NetCoreApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreApp.dll"]