FROM mcr.microsoft.com/dotnet/core/runtime:3.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["IoT.Simulator/IoT.Simulator.csproj", "IoT.Simulator/"]
RUN dotnet restore "IoT.Simulator/IoT.Simulator.csproj"
COPY . .
WORKDIR "/src/IoT.Simulator"
RUN dotnet build "IoT.Simulator.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "IoT.Simulator.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "IoT.Simulator.dll"]