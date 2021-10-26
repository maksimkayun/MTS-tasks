FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BreakMeDown/BreakMeDown.csproj", "BreakMeDown/"]
RUN dotnet restore "BreakMeDown/BreakMeDown.csproj"
COPY . .
WORKDIR "/src/BreakMeDown"
RUN dotnet build "BreakMeDown.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BreakMeDown.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BreakMeDown.dll"]
