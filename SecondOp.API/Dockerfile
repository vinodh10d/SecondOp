FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SecondOp.API/SecondOp.API.csproj", "SecondOp.API/"]
RUN dotnet restore "SecondOp.API/SecondOp.API.csproj"
COPY . .
WORKDIR "/src/SecondOp.API"
RUN dotnet build "SecondOp.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondOp.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondOp.API.dll"]
