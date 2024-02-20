FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 5089

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY  ["PostgreSqlDotnetCore.csproj", "."]
RUN dotnet restore "PostgreSqlDotnetCore.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "PostgreSqlDotnetCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish  "PostgreSqlDotnetCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PostgreSqlDotnetCore.dll"]