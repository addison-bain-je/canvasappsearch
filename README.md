# canvasappsearch
Implementation of different custom search types for Canvas App gallery

![](https://github.com/addison-bain-je/canvasappsearch/blob/main/SearchTypes.gif)

Additive Search/
For the Items property in the gallery:/
```
ForAll(
Distinct(
Ungroup(
   ForAll(
      Split(
         SearchInput1.Text,
         ";"
      ),
      Filter(
         Collection1,
         TrimEnds(Value) in Product || TrimEnds(Value) in Color
      )
   ),
   Value
),ThisRecord),Value)

```

