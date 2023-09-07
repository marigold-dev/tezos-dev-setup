FROM ghcr.io/dipdup-io/metadata:latest as dipdup-build

FROM scratch
WORKDIR /app/metadata/

COPY --from=dipdup-build /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=dipdup-build /go/bin/dipdup-metadata /go/bin/dipdup-metadata
COPY --from=dipdup-build /app/metadata/mappings ./mappings
COPY --from=dipdup-build /app/metadata/graphql ./graphql
COPY --from=dipdup-build /app/metadata/views/*.sql ./views/
COPY --from=dipdup-build /app/metadata/sql/*.sql ./sql/
COPY --from=dipdup-build /app/metadata/custom_hasura_config ./custom_hasura_config

COPY ./dipdup/dipdup.yml ./dipdup.yml

ENTRYPOINT ["/go/bin/dipdup-metadata"]
