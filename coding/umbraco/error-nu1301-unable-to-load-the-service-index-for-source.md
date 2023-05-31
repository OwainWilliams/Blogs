---
description: An error that appears when trying to setup a new site.
---

# error NU1301: Unable to load the service index for source

`error NU1301: Unable to load the service index for source` [`https://pkgs.dev.azure.com/internal/_packaging/Internal.Nuget/nuget/v3/index.json.`](https://pkgs.dev.azure.com/spindogs/\_packaging/Spindogs.Nuget/nuget/v3/index.json.)\




How to fix - in your terminal enter this:&#x20;

```
dotnet restore --interactive
```
