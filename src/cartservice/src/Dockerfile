FROM mcr.microsoft.com/dotnet/sdk:9.0 AS builder

WORKDIR /app

COPY cartservice.csproj .

RUN dotnet restore 

COPY . .

RUN dotnet publish -c Release --self-contained true -p:PublishSingleFile=true -p:PublishTrimmed=true -o /cart

FROM mcr.microsoft.com/dotnet/runtime-deps:9.0 AS runner

WORKDIR /app

COPY --from=builder /cart .

EXPOSE 8081

ENV ASPNETCORE_HTTP_PORTS=8081

USER 1000

ENTRYPOINT ["/app/cartservice"]




