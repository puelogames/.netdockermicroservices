FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
ENV ASPNETCORE_URLS http://+:82
EXPOSE 82

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MicroService2/MicroService2.csproj", "MicroService2/"]
RUN dotnet restore "MicroService2/MicroService2.csproj"
COPY . .
WORKDIR "/src/MicroService2"
RUN dotnet build "MicroService2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroService2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroService2.dll"]