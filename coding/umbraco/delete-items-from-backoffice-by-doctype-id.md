# Delete items from backoffice by DocType ID

This deletes all content from the Root of the site that has a Document Type ID of 1097.

```text
@{
    var contentService = Current.Services.ContentService;

    var RootNode = Model.Root().Children();

    foreach(var node in RootNode)
    {

        contentService.DeleteOfType(1097);

    }


}

```

