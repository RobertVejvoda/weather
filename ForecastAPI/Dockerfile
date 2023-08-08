FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Healthchecks", "Healthchecks/"]
COPY ["ForecastAPI/ForecastAPI.csproj", "ForecastAPI/"]
RUN dotnet restore "ForecastAPI/ForecastAPI.csproj"
COPY . .
WORKDIR "/src/ForecastAPI"
RUN dotnet build "ForecastAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ForecastAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ForecastAPI.dll"]
