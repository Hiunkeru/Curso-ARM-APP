#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["curso-arm-docker-mvc/curso-arm-docker-mvc.csproj", "curso-arm-docker-mvc/"]
RUN dotnet restore "curso-arm-docker-mvc/curso-arm-docker-mvc.csproj"
COPY . .
WORKDIR "/src/curso-arm-docker-mvc"
RUN dotnet build "curso-arm-docker-mvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "curso-arm-docker-mvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "curso-arm-docker-mvc.dll"]