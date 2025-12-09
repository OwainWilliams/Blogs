# How to Strongly Type to Models

OLD: <br>

```
case VideoItem.ModelTypeAlias:
                        if (article.HasValue("contentLabel"))
                        {
                            docType = article.GetPropertyValue<IPublishedContent>("contentLabel").Name;
                            break;
                        }
                        else
                        {
                            docType = "Video";
                            break;
                        }
```

New:&#x20;

```
case VideoItem.ModelTypeAlias:
    docType = "Video";
    if(article is VideoItem videoItem && videoItem.ContentLabel != null)
    {
       docType = videoItem.ContentLabel.Name;
    }
```
