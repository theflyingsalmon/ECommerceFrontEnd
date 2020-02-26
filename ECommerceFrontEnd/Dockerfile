#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ECommerceFrontEnd/ECommerceFrontEnd.csproj", "ECommerceFrontEnd/"]
RUN dotnet restore "ECommerceFrontEnd/ECommerceFrontEnd.csproj"
COPY . .
WORKDIR "/src/ECommerceFrontEnd"
RUN dotnet build "ECommerceFrontEnd.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ECommerceFrontEnd.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ECommerceFrontEnd.dll"]
