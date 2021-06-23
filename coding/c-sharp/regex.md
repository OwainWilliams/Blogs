---
description: Some useful Regex examples
---

# Regex

Check if a value starts with a number: 

```text
  @using System.Text.RegularExpressions
  
      string patternStartsWithNumber = @"^(?:[0-9])";
      
      
  @if (!vacancy.VacancySalary.IsNullOrWhiteSpace() && Regex.Match(vacancy.VacancySalary, patternStartsWithNumber).Success)
                        {
                        }
```

