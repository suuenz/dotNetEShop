# ---------- Build ----------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ./src/Web/Web.csproj ./Web/
RUN dotnet restore ./Web/Web.csproj
COPY ./src/Web/ ./Web/
WORKDIR /src/Web
RUN dotnet publish -c Release -o /app/out

# ---------- Runtime ----------
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
# مهم: اپ روی 8080 گوش بده
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080
COPY --from=build /app/out .
ENTRYPOINT ["dotnet","Web.dll"]
