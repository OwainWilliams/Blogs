---
description: Adding content programatically to the back office
---

# Adding content to the backoffice

Full blog : [https://owain.codes/blog/posts/2020/october/add-content-programmatically-to-umbraco-8/](https://owain.codes/blog/posts/2020/october/add-content-programmatically-to-umbraco-8/)

  
Place this code on to a view of the parent node in the backoffice. 

Root   
-&gt; Parent Node   
--&gt; Child. 

This example makes a mix of BlogArticles and NewsArticles under the parent node. 

```text
@using Umbraco.Core.Composing;
@using System;
```

```text
  
//Used to mass create content in the backoffice.
    var contentService = Current.Services.ContentService;
 
    // This is the id of the 'folder' you want to copy.
    // Place a child within the folder and it will be replicated
    var parentNodeId = Model.Id;
    var titleHeadings = new string[]
            {​​​​​​​​
               "rainstorm","preach","weary","gun","plain","zany","helpful","long","various","development","foamy","melted","narrow","freezing","reduce","burly","price","curl","bell",
                "distribution","glow","turkey","meddle","men","boundless","scratch","excuse","mature","post","file","unsuitable","writer","eatable","magical","mere","tray","bump","spotted",
            "volcano","squash","hushed","maddening","smooth","edge","tongue","scorch","gainful","please","decide","porter","jaded","ski","yoke","hospital","mask","barbarous","bubble","business",
            "normal","ashamed","underwear","superb","bore","tedious","beginner","pigs","disagree","earth","verse","perpetual","scattered","rhetorical","workable","cuddly","furry","seemly","puzzled","load",
            "sloppy","ludicrous","queen","ethereal","religion","psychotic","nifty","puzzling","truthful","connection","vulgar","lumpy","bake","bike","mixed","clover","flag","deafening","soak","flaky","statement","lucky"
                     }​​​​​​​​;
    var baseDate = DateTime.Today;
 
    // Keep this < n low, remember it replicates the folder so 1, 2, 4, 8, 16, 32 items are created for 5 loops.
    for (var i = 0; i < 300; i++)
    {​​​​​​​​
        Random rnd = new Random(DateTime.Now.Millisecond);
        var name = "Read about " + titleHeadings[rnd.Next(titleHeadings.Length)];
        var date = DateTime.Today.AddDays((rnd.NextDouble() * (28 - 1) + 1) * -1 ).AddMonths(rnd.Next(0, 12) * -1).AddYears(rnd.Next(0, 2) * -1);
        var contentType = rnd.Next(1, 2) == 1 ? BlogArticle.ModelTypeAlias : NewsArticle.ModelTypeAlias;
        var node = contentService.Create(name, parentNodeId, contentType);
        node.SetValue(Article.GetModelPropertyType(a => a.Title).Alias, name);
        node.SetValue(Article.GetModelPropertyType(a => a.PublishDate).Alias, date);
 
        contentService.SaveAndPublish(node);
    }​​​​​​​​
```

