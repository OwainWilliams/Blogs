---
description: Represents a collection of keys and values.
---

# Dictionary&lt;Tkey, TValue&gt;

**Added 04/11/2020**   
Working with dictionaries for adding a filter value to the backoffice of Umbraco on CAS.



`TKey` - The type of the keys in the dictionary.

`TValue` - The type of the values in the dictionary.



```text
// Create a new dictionary of strings, with string keys.
//
Dictionary<string, string> openWith =
    new Dictionary<string, string>();

// Add some elements to the dictionary. There are no
// duplicate keys, but some of the values are duplicates.
openWith.Add("txt", "notepad.exe");
openWith.Add("bmp", "paint.exe");
openWith.Add("dib", "paint.exe");
openWith.Add("rtf", "wordpad.exe");

```

 The [Dictionary&lt;TKey,TValue&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netframework-4.8) generic class provides a mapping from a set of keys to a set of values. Each addition to the dictionary consists of a value and its associated key. Retrieving a value by using its key is very fast, close to O\(1\), because the [Dictionary&lt;TKey,TValue&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netframework-4.8) class is implemented as a hash table.

```text
using System;
using System.Collections.Generic;

public class Program
{
	public static void Main()
	{
		Dictionary<string, string> openWith = new Dictionary<string, string>();
		// Add some elements to the dictionary. There are no
		// duplicate keys, but some of the values are duplicates.
		openWith.Add("txt", "notepad.exe");
		openWith.Add("bmp", "paint.exe");
		openWith.Add("dib", "paint.exe");
		openWith.Add("rtf", "wordpad.exe");
		
		foreach (KeyValuePair<string, string> kvp in openWith)
		{
			Console.WriteLine("Key = {0}, Value = {1}", kvp.Key, kvp.Value);
		}
	}
}
```

