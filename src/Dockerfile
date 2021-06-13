FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build-env
WORKDIR /app

COPY . .
RUN dotnet restore \
    &&  dotnet publish MyWebApp/MyWebApp.csproj -c Release -o out --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /app
COPY --from=build-env /app/out/ .
ENTRYPOINT ["dotnet", "MyWebApp.dll"]