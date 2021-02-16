# Build up SQL statements

```text
   var sql = scope.SqlContext.Sql().Select("*")
                        .From<DownloadsEntry>();
                    if (dateRange.From.HasValue)
                        sql.Where<DownloadsEntry>(d => d.DownloadDate >= dateRange.From.Value);
                    if(dateRange.To.HasValue)
                        sql.Where<DownloadsEntry>(d => d.DownloadDate < dateRange.To.Value);

```

Only works if you want AND clauses between the Wheres

