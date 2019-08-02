FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
ENV ASPNETCORE_URLS http://+:83
EXPOSE 83

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MicroService3/MicroService3.csproj", "MicroService3/"]
RUN dotnet restore "MicroService3/MicroService3.csproj"
COPY . .
WORKDIR "/src/MicroService3"
RUN dotnet build "MicroService3.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroService3.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroService3.dll"]