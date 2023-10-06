FROM golang:1.21-alpine3.18

RUN go install github.com/cosmtrek/air@latest && \
    go install github.com/bufbuild/buf/cmd/buf@latest && \
    go install github.com/volatiletech/sqlboiler/v4@latest && \
    go install github.com/volatiletech/sqlboiler/v4/drivers/sqlboiler-psql@latest && \
    go install github.com/volatiletech/sqlboiler/v4/drivers/sqlboiler-sqlite3@latest && \
    go clean -cache -modcache -testcache -fuzzcache
