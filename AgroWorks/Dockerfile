FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["AgroWorks/AgroWorks.csproj", "AgroWorks/"]
RUN dotnet restore "AgroWorks/AgroWorks.csproj"
COPY . .
WORKDIR "/src/AgroWorks"
RUN dotnet build "AgroWorks.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AgroWorks.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AgroWorks.dll"]
