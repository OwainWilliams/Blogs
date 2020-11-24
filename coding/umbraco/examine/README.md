---
description: The search engine used within Umbraco
---

# Examine

* [https://shazwazza.github.io/Examine/](https://shazwazza.github.io/Examine/) 

{% tabs %}
{% tab title="Add custom field to the Index" %}
```text
IndexerComponent : IComponent

Public void Initialize()
{
   externalIndex.FieldDefinitionCollection.AddOrUpdate(new FieldDefinition("FieldName", "FieldDataOrContent"));
}

```
{% endtab %}

{% tab title="Add content to custom field" %}
In the same file - `IndexerComponent.cs`

```text
   private void IndexResourceSpecificProperties(IndexingItemEventArgs e, ResourceItem resourceItem)
        {
            try
            {
                var resourceDate = resourceItem.ResourceDate;
                e.ValueSet.Add(Constants.Resources.ResourceDateSortableExamineField, resourceDate.Ticks);
```
{% endtab %}
{% endtabs %}



