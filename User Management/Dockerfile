#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["User Management/User Management.csproj", "User Management/"]
RUN dotnet restore "User Management/User Management.csproj"
COPY . .
WORKDIR "/src/User Management"
RUN dotnet build "User Management.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "User Management.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "User Management.dll"]