# Use a minimal .NET 8 SDK image as the base
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the csproj and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the project
COPY . .

# Build the application
RUN dotnet publish -c Release -o out

# Use a minimal .NET 8 runtime image as the base
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Expose the port used by the application
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "WebApplication3.dll"]