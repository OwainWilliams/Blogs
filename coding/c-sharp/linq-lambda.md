# Linq / Lambda

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

The ToModel method returns a IEnumberble of SitemapNodeModel, ToModel accepted a T of IEnumberable IPublishedcontent.&#x20;

I need to remove ToModel so I wrote the following :&#x20;

```


List<SitemapNodeModel> list = new List<SitemapNodeModel>();

foreach (var child in children)
{
				SitemapNodeModel sitemap = new SitemapNodeModel
				{
					Id = child.Id,
					Name = child.Name,
					DocumentTypeAlias = child.DocumentTypeAlias,
					Url = child.Url,
					UrlName = child.UrlName,
					UpdateDate = child.UpdateDate
				};
				
				list.Add(sitemap);
}
```

This works but it can also be done with Linq and Lambda&#x20;

```
var children = _umbracoWrapper.Descendants(root)
				.Where(x => _umbracoWrapper.GetPropertyValue<bool>(x, "metaSitemap"))
				.Select(child => new SitemapNodeModel
				{
					Id = child.Id,
					Name = child.Name,
					DocumentTypeAlias = child.DocumentTypeAlias,
					Url = child.Url,
					UrlName = child.UrlName,
					UpdateDate = child.UpdateDate
				}).ToList();



var umbracoNodes = new List<SitemapNodeModel>(children);
```
