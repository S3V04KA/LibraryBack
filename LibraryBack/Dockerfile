FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LibraryBack/LibraryBack.csproj", "LibraryBack/"]
RUN dotnet restore "LibraryBack/LibraryBack.csproj"
COPY . .
WORKDIR "/src/LibraryBack"
RUN dotnet build "LibraryBack.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LibraryBack.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LibraryBack.dll"]
