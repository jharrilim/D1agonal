FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["D1agonal.Lookup/D1agonal.Lookup.csproj", "D1agonal.Lookup/"]
RUN dotnet restore "D1agonal.Lookup/D1agonal.Lookup.csproj"
COPY . .
WORKDIR "/src/D1agonal.Lookup"
RUN dotnet build "D1agonal.Lookup.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "D1agonal.Lookup.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "D1agonal.Lookup.dll"]