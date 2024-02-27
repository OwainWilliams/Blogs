# Alt Tag

Only show an `alt` tag if there is a value.

```csharp
var altText = Model.BackgroundImage.Value("altText")

<img src="a_source_for_the_image" @(altText.IsNullOrWhiteSpace() ? null : @Html.Raw($"alt=\"{altText}\"")) />
```
