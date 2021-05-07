# Strongly Type

OLD:   


```text
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

New: 

```text
case VideoItem.ModelTypeAlias:
    docType = "Video";
    if(article is VideoItem videoItem && videoItem.ContentLabel != null)
    {
       docType = videoItem.ContentLabel.Name;
    }
```

