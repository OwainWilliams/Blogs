---
description: How to get the current rendered page document (content) type.
---

# Get the current page content type alias

Imagine you have a masterpage which calls a searchbar partial view. The masterpage can be used on any page and the partial passes the SiteRoot model to the partial

```
@{
  var siteSettings = Model.Root() as SiteRoot;
}
  
<partial name="master/_header" model="siteSettings" />
```

The \_header will always have the model type of SiteRoot but if you are on a results page for example then you might want to do something specific e.g. hide the search bar because there is a search bar already on the search results page.&#x20;

You can check what page your partial is being rendered on like so :

```
@inherits UmbracoViewPage
@{
 var siteSettings = Model.Root() as SiteRoot;
var isResultsPage = UmbracoContext.PublishedRequest.PublishedContent.ContentType.Alias == SearchResults.ModelTypeAlias;
}
```
