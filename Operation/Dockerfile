FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Operation/Operation.csproj", "Operation/"]
RUN dotnet restore "Operation/Operation.csproj"
COPY . .
WORKDIR "/src/Operation"
RUN dotnet build "Operation.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Operation.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Operation.dll"]
