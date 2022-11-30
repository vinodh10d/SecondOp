FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SecondOp.Web.Website/SecondOp.Web.Website.csproj", "SecondOp.Web.Website/"]
RUN dotnet restore "SecondOp.Web.Website/SecondOp.Web.Website.csproj"
COPY . .
WORKDIR "/src/SecondOp.Web.Website"
RUN dotnet build "SecondOp.Web.Website.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondOp.Web.Website.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondOp.Web.Website.dll"]
