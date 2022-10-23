FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Src/Web/Company.Crm.Web.Mvc/Company.Crm.Web.Mvc.csproj", "Company.Crm.Web.Mvc/"]
RUN dotnet restore "Src/Web/Company.Crm.Web.Mvc/Company.Crm.Web.Mvc.csproj"
COPY . .
WORKDIR "/src/Company.Crm.Web.Mvc"
RUN dotnet build "Company.Crm.Web.Mvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Company.Crm.Web.Mvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Company.Crm.Web.Mvc.dll"]
