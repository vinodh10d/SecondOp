FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SecondOp.App.Api/SecondOp.App.Api.csproj", "SecondOp.App.Api/"]
RUN dotnet restore "SecondOp.App.Api/SecondOp.App.Api.csproj"
COPY . .
WORKDIR "/src/SecondOp.App.Api"
RUN dotnet build "SecondOp.App.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondOp.App.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondOp.App.Api.dll"]
