# .NET SDK for Workshop

A development environment for .NET projects. It provides the .NET
toolchain via a versioned content snap, persists NuGet packages and
.NET runtime data on the host to speed up builds across workshop updates,
and gives you standard `dotnet` CLI commands for building, testing, and running
your applications. Multiple .NET versions are available via separate channels
(e.g. `8/stable`, `9/stable`, `10/stable`).

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: dotnet-app
base: ubuntu@24.04
sdks:
  - name: dotnet
    channel: 8/stable

actions:
  build: |
    dotnet build
  test: |
    dotnet test
```

This demonstrates a basic .NET build workflow with persistent NuGet caching.

---

## Using the SDK

### Prerequisites, project layout

1. No prerequisite SDKs are required.
2. Your .NET project (with a `.csproj` or `.sln` file) should be in your
   project directory:

   ```bash
   git clone <YOUR_REPO_URL>
   ```

3. On launch, the SDK configures `PATH`. No dependencies are pre-installed;
   NuGet packages are downloaded during the first `dotnet build` or
   `dotnet restore`.

### Build the project

Once the workshop is ready:

```bash
workshop shell
dotnet build
```

The first build downloads NuGet packages into `~/.nuget`, which is mapped to
your host via the `nuget-cache` mount plug. Subsequent builds reuse cached
packages.

To see where the NuGet cache is stored on the host:

```bash
workshop info
```

### Test and run

From within the workshop shell:

```bash
workshop shell
dotnet test
dotnet run
```

Use standard `dotnet` commands; the toolchain behaves exactly as it would in a
regular .NET installation.

---

## Plugs (resources this SDK consumes)

### `nuget-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.nuget`
- Purpose: Persists NuGet package downloads between workshop updates.

### `dotnet-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.dotnet`
- Purpose: Persists .NET tools and runtime data between workshop updates.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [.NET official documentation](https://learn.microsoft.com/en-us/dotnet/)
- [NuGet documentation](https://learn.microsoft.com/en-us/nuget/)
- [Workshop documentation](https://canonical-workshop.readthedocs-hosted.com/latest/)

---

## Community and support

- .NET community:
  [.NET Community Forum](https://dotnetfoundation.org/community)
- Workshop forum:
  [Workshop Discourse](https://discourse.canonical.com/c/engineering/workshops/34)
- Please review our
  [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct) before
  participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See `CONTRIBUTING.md` for guidelines.
- Open issues or pull requests on the official repository.

---

## License and copyright

Copyright 2025 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under
the terms of the
[GNU Lesser General Public License version 2.1 (LGPLv2.1)](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
as published by the Free Software Foundation.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

The .NET runtime and SDK are licensed under
[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
