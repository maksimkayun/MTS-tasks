FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["HigherSorting/HigherSorting.csproj", "HigherSorting/"]
RUN dotnet restore "HigherSorting/HigherSorting.csproj"
COPY . .
WORKDIR "/src/HigherSorting"
RUN dotnet build "HigherSorting.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HigherSorting.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HigherSorting.dll"]
