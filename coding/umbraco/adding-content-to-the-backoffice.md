---
description: Adding content programatically to the back office
---

# Adding content to the backoffice

Full blog : [https://owain.codes/blog/posts/2020/october/add-content-programmatically-to-umbraco-8/](https://owain.codes/blog/posts/2020/october/add-content-programmatically-to-umbraco-8/)

### Adding content with random Page titles.

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

### Adding random postcodes to the content

Another example - this time adding random postcodes in to the content. 

```text



    //Used to mass create content in the backoffice.
    var contentService = Current.Services.ContentService;

    // This is the id of the 'folder' you want to copy.
    // Place a child within the folder and it will be replicated
    var parentNodeId = Model.Id;
    var titleHeadings = new string[] { "rainstorm", "preach", "weary", "gun", "plain", "zany", "helpful", "long", "various", "development", "foamy", "melted", "narrow", "freezing", "reduce", "burly", "price", "curl", "bell", "distribution", "glow", "turkey", "meddle", "men", "boundless", "scratch", "excuse", "mature", "post", "file", "unsuitable", "writer", "eatable", "magical", "mere", "tray", "bump", "spotted", "volcano", "squash", "hushed", "maddening", "smooth", "edge", "tongue", "scorch", "gainful", "please", "decide", "porter", "jaded", "ski", "yoke", "hospital", "mask", "barbarous", "bubble", "business", "normal", "ashamed", "underwear", "superb", "bore", "tedious", "beginner", "pigs", "disagree", "earth", "verse", "perpetual", "scattered", "rhetorical", "workable", "cuddly", "furry", "seemly", "puzzled", "load", "sloppy", "ludicrous", "queen", "ethereal", "religion", "psychotic", "nifty", "puzzling", "truthful", "connection", "vulgar", "lumpy", "bake", "bike", "mixed", "clover", "flag", "deafening", "soak", "flaky", "statement", "lucky" };
    var postcodes = new string[]{"B15 1AZ","NE63 8JX","RH17 5EZ","BT32 9AY","SG7 6RG","SS8 7QN","DD2 4LU","LL18 4NG","B43 7EU","G64 2JZ","CF23 9JP","DN14 8JD","M24 1JP","OL9 0LW","SG5 1HX","PO31 7FL","GU24 9PP","B64 5RU","B31 1SE","SR8 5TB","WN3 6PF","PO12 3BP","PA12 4AD","M34 6HL","DG2 0RH","BT37 9SB","SY6 7EY","SA10 6DE","BS24 7FB","MK43 0SD","BB7 9NX","B62 9RJ","NR5 8HT","TN12 0AD","KY2 5XQ","LD1 5UW","L20 0BQ","TQ2 7GA"};

    var baseDate = DateTime.Today;

    // Keep this < n low, remember it replicates the folder so 1, 2, 4, 8, 16, 32 items are created for 5 loops.
    for (var i = 0; i < 300; i++)
    {
        Random rnd = new Random(DateTime.Now.Millisecond);
        var name = "Event " + titleHeadings[rnd.Next(titleHeadings.Length)];
        var date = DateTime.Today.AddDays((rnd.NextDouble() * (28 - 1) + 1) * -1).AddMonths(rnd.Next(0, 12) * -1).AddYears(rnd.Next(0, 2) * -1);
        var endDate = DateTime.Today.AddDays((rnd.NextDouble() * (28 - 1) + 1) * -1).AddMonths(rnd.Next(0, 12) * -1).AddYears(rnd.Next(0, 2) * -1);
        var postcode = postcodes[rnd.Next(postcodes.Length)];
        //var contentType = rnd.Next(1, 2) == 1 ? BlogArticle.ModelTypeAlias : NewsArticle.ModelTypeAlias;
        var node = contentService.Create(name, parentNodeId, EventItem.ModelTypeAlias);
        node.SetValue(EventItem.GetModelPropertyType(a => a.Title).Alias, name);
        node.SetValue(EventItem.GetModelPropertyType(a => a.EventStartDate).Alias, date);
        node.SetValue(EventItem.GetModelPropertyType(a => a.EventEndDate).Alias, endDate);
        node.SetValue(EventItem.GetModelPropertyType(a => a.AddressPostcode).Alias, postcode);

        contentService.SaveAndPublish(node);
```



