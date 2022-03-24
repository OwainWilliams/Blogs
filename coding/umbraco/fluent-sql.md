# Fluent SQL

```
 using Umbraco.Core.Persistence;
 
 using (var scope = _scopeProvider.CreateScope())
            {
                var sql = scope.SqlContext.Sql().Select("Keyword, Definition").From<GlossaryItem>()
                    .Where<GlossaryItem>(g => g.Language == culture);
                
                var glossaryDefinitions = scope.Database.Query<GlossaryItem>(sql);
                return glossaryDefinitions;
            }
```
