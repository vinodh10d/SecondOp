FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Second.StatusCheck.WorkerService/Second.StatusCheck.WorkerService.csproj", "Second.StatusCheck.WorkerService/"]
RUN dotnet restore "Second.StatusCheck.WorkerService/Second.StatusCheck.WorkerService.csproj"
COPY . .
WORKDIR "/src/Second.StatusCheck.WorkerService"
RUN dotnet build "Second.StatusCheck.WorkerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Second.StatusCheck.WorkerService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Second.StatusCheck.WorkerService.dll"]
