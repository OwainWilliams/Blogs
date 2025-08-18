---
description: >-
  If you want to add a bit more user friendliness to your Blocklist here is a
  handy bit of code :
---

# Dynamic BlockList Label

```
{{ imageCards.contentData.length == 1 ? imageCards.contentData.length + ' Image Copy card' : imageCards.contentData.length + 'Image Copy cards' }}
```

In this example, it counts how many imageCards I have on a blocklist and shows a different label depending on the number. imageCards is the alias on the element block : \
\
![](<../../../.gitbook/assets/image (2).png>)

&#x20;I can add as many "image cards" to this property as I like.&#x20;

This is how it displays&#x20;

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

