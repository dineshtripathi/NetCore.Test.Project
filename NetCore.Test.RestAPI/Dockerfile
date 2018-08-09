FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 7307
EXPOSE 44366

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY NetCore.Test.RestAPI/NetCore.Test.RestAPI.csproj NetCore.Test.RestAPI/
RUN dotnet restore NetCore.Test.RestAPI/NetCore.Test.RestAPI.csproj
COPY . .
WORKDIR /src/NetCore.Test.RestAPI
RUN dotnet build NetCore.Test.RestAPI.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCore.Test.RestAPI.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCore.Test.RestAPI.dll"]
