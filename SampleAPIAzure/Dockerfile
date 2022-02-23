#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SampleAPIAzure/SampleAPIAzure.csproj", "SampleAPIAzure/"]
RUN dotnet restore "SampleAPIAzure/SampleAPIAzure.csproj"
COPY . .
WORKDIR "/src/SampleAPIAzure"
RUN dotnet build "SampleAPIAzure.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SampleAPIAzure.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SampleAPIAzure.dll"]