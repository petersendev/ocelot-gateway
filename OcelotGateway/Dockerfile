FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src

COPY OcelotGateway.csproj .
RUN dotnet restore OcelotGateway.csproj
COPY . .
RUN dotnet build OcelotGateway.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish OcelotGateway.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OcelotGateway.dll"]