---
description: Need to find out the parent model type from a partial?
---

# Find out Model of Current page

On the partial view use <br>

`if(Umbraco.AssignedContentItem is PropertyListing) { bannerClass += "__property"; }`\
\
This then checks to see if the current page that this partial is on and if it's of type PropertyListing then I add the \
`__property` css class
