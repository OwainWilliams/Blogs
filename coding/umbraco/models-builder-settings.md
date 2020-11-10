# Models Builder Settings

### Setting up Models Builder within web.config to save the models to a custom folder.

If using this, you need to leave out the `value` for line \#4 and \#5

```text
  <add key="Umbraco.ModelsBuilder.Enable" value="true" />
  <add key="Umbraco.ModelsBuilder.ModelsMode" value="AppData" />

  <add key="Umbraco.ModelsBuilder.AcceptUnsafeModelsDirectory" value="true" />
  <add key="Umbraco.ModelsBuilder.ModelsDirectory" value="~/Models/Generated" />
```

