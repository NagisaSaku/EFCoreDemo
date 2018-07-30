FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY EFCoreDemo/EFCoreDemo.csproj EFCoreDemo/
RUN dotnet restore EFCoreDemo/EFCoreDemo.csproj
COPY . .
WORKDIR /src/EFCoreDemo
RUN dotnet build EFCoreDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish EFCoreDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EFCoreDemo.dll"]
