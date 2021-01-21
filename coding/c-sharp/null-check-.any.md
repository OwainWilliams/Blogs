# Null check .any\(\)

You can't just have 

```text
if(content.Any())
{
    // Do something
}
```

The reason is if there is no content then there is nothing to count and do it doesn't exist which means content is equal to null

To combat that you need to null check it. 

```text
 @if (content != null && content.Any())
 {
  // do something
 }
  
```

