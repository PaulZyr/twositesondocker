#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["First.Web/First.Web.csproj", "First.Web/"]
RUN dotnet restore "First.Web/First.Web.csproj"
COPY . .
WORKDIR "/src/First.Web"
RUN dotnet build "First.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "First.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "First.Web.dll"]