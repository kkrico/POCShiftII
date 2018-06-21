FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY POCShiftII/POCShiftII.csproj POCShiftII/
RUN dotnet restore POCShiftII/POCShiftII.csproj
COPY . .
WORKDIR /src/POCShiftII
RUN dotnet build POCShiftII.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish POCShiftII.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "POCShiftII.dll"]
