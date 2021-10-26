FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BeOrNotToBe/BeOrNotToBe.csproj", "BeOrNotToBe/"]
RUN dotnet restore "BeOrNotToBe/BeOrNotToBe.csproj"
COPY . .
WORKDIR "/src/BeOrNotToBe"
RUN dotnet build "BeOrNotToBe.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BeOrNotToBe.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BeOrNotToBe.dll"]
