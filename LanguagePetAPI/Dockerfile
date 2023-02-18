FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["LanguagePetAPI/LanguagePetAPI.csproj", "LanguagePetAPI/"]
RUN dotnet restore "LanguagePetAPI/LanguagePetAPI.csproj"
COPY . .
WORKDIR "/src/LanguagePetAPI"
RUN dotnet build "LanguagePetAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LanguagePetAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LanguagePetAPI.dll"]
