#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 3000
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LPGManager/LPGManager.csproj", "LPGManager/"]
RUN dotnet restore "LPGManager/LPGManager.csproj"
COPY . .
WORKDIR "/src/LPGManager"
RUN dotnet build "LPGManager.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LPGManager.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LPGManager.dll"]

#help
#docker pull sajidur07/lpgmanager:latest
#docker run -p 3000:3000 sajidur07/lpgmanager:latest
