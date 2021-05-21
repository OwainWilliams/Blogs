---
description: Umbraco.TypedContent
---

# Working with IPublishedContent

```text
public ActionResult GetDistinctContentTypesForAuthor(string authorId)
        {
            //Create an empty list of type String
            List<string> allResults = new List<string>();

            // Setup what Search Index to use
            var searcher = ExamineManager.Instance.SearchProviderCollection["ContentHubSearcher"];

            // Tell the search what will be searched, this is content that will be searched
            ISearchCriteria searchCriteria = searcher.CreateSearchCriteria(IndexTypes.Content);

            
            // Create the lucene query, this is looking for all authors with the a matching authorId
            // within lucene, author is stored as an Key e.g. author: 9e0dad13195243389215ce452031ffb5
            
            IBooleanOperation query = searchCriteria.GroupedOr(new string[] { "author" }, authorId);

            // Run the search within Examine
            var queryResults = searcher.Search(query.Compile());

            // from the results, select all the Ids and save them in IEnumerable
            IEnumerable<int> nodeIds = queryResults.Select(x => x.Id);
            
            // Create a List of IPublishedContent using Umbraco.TypedContent and the IEnumberable nodeIds List
            List<IPublishedContent> publishedContent = Umbraco.TypedContent(nodeIds).ToList();

            
            // With the List of IPublishedContent - do what you need to do.
            if (publishedContent != null)
            {
                foreach (var item in publishedContent)
                {

                    if (item is GenericContent genericContent && genericContent.ContentLabel is GenericPageLabel pageLabel)
                    {
                        allResults.Add(pageLabel.LabelTitle.IfNullOrWhiteSpace(pageLabel.Name));
                    }
                    else if (item is VideoItem videoItem && videoItem.ContentLabel is GenericPageLabel videoPageLabel)
                    {
                        allResults.Add(videoPageLabel.LabelTitle.IfNullOrWhiteSpace(videoPageLabel.Name));
                    }
                    else if (item is WebinarContent webinarItem && webinarItem.ContentLabel is GenericPageLabel webinarPageLabel)
                    {
                        allResults.Add(webinarPageLabel.LabelTitle.IfNullOrWhiteSpace(webinarPageLabel.Name));
                    }
                    else if (item is StoryContent storyItem && storyItem.ContentLabel is GenericPageLabel storyPageLabel)
                    {
                        allResults.Add(storyPageLabel.LabelTitle.IfNullOrWhiteSpace(storyPageLabel.Name));
                    }
                    else
                    {
                        allResults.Add(Global.FriendlyFromDocTypeAlias(item.DocumentTypeAlias));
                    }
                }
            }


            return PartialView("Authors/ContentTypesDropdown", allResults.Distinct().OrderBy(x => x));


        }
```

