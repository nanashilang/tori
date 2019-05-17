FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["proj_test/proj_test.csproj", "proj_test/"]
RUN dotnet restore "proj_test/proj_test.csproj"
COPY . .
WORKDIR "/src/proj_test"
RUN dotnet build "proj_test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "proj_test.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "proj_test.dll"]