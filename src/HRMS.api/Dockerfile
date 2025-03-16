# Build Stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the .csproj file into the HRMS.api directory
COPY HRMS.api.csproj ./HRMS.api/
RUN dotnet restore "HRMS.api/HRMS.api.csproj"

# Copy the remaining files into the HRMS.api directory
COPY . ./HRMS.api/
WORKDIR /src/HRMS.api
RUN dotnet publish "HRMS.api.csproj" -c Release -o /app/publish

# Final Runtime Stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy the published output to /app
COPY --from=build /app/publish .

# Set environment variable for ports
ENV ASPNETCORE_HTTP_PORTS=5000
EXPOSE 5000

# Start the application
ENTRYPOINT ["dotnet", "HRMS.api.dll"]
