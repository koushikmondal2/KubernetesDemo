#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

COPY *.csproj ./

RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out /property:PublishWithAspNetCoreTargetManifest=false


FROM FROM mcr.microsoft.com/dotnet/core/aspnet:3.1.8 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

ENTRYPOINT ["dotnet", "Kubernetes.dll"]