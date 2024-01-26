FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["branching/branching.csproj", "branching/"]
RUN dotnet restore "branching/branching.csproj"
COPY . .
WORKDIR "/src/branching"
RUN dotnet build "branching.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "branching.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "branching.dll"]
