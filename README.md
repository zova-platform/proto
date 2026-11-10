# proto

gRPC and event contracts for every ZOVA service. This repo is the source of truth for internal APIs.

## Layout

```text
zova/<service>/v1/<service>.proto   # source
gen/go/zova/<service>/v1/           # generated Go code (committed)
```

Package names follow `zova.<service>.v1`. Generated Go import path:

```go
import commonv1 "github.com/zova-platform/proto/gen/go/zova/common/v1"
```

## Use from a service

```bash
go get github.com/zova-platform/proto@v0.1.0
```

## Develop

Requires [Buf](https://buf.build/docs/installation) and [Task](https://taskfile.dev).

```bash
task lint       # format check + lint
task gen        # regenerate gen/go
task breaking   # compare with main
task check      # everything CI runs
```

Plugin versions (`protoc-gen-go`, `protoc-gen-go-grpc`) are pinned as Go tools in `go.mod`.

## Rules

- Never change a field number or type. Add new fields, reserve removed ones.
- A breaking change means a new package version (`zova.trip.v2`).
- Every change gets a SemVer tag so services can upgrade on their own schedule.
