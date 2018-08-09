FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 7664
EXPOSE 44379

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY NetCore.Test.AspNetCore/NetCore.Test.AspNetCore.csproj NetCore.Test.AspNetCore/
RUN dotnet restore NetCore.Test.AspNetCore/NetCore.Test.AspNetCore.csproj
COPY . .
WORKDIR /src/NetCore.Test.AspNetCore
RUN dotnet build NetCore.Test.AspNetCore.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NetCore.Test.AspNetCore.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCore.Test.AspNetCore.dll"]
