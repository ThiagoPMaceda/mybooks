FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["packages/api/MyBooks.csproj", "packages/api/"]
RUN dotnet restore "packages/api/MyBooks.csproj"
COPY . .
WORKDIR "/src/packages/api"
RUN dotnet build "MyBooks.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyBooks.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyBooks.dll"]
