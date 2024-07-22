# canvasappsearch
Implementation of different custom search types for Canvas App gallery

![](https://github.com/addison-bain-je/canvasappsearch/blob/main/SearchTypes.gif)


Additive Search\
For the Items property in the gallery:
```
ForAll(
Distinct(
Ungroup(
   ForAll(
      Split(
         SearchInput1.Text,
         ";" //or any delimiter.
      ),
      Filter(
         Collection1,
         TrimEnds(Value) in Product || TrimEnds(Value) in Color  // and more columns etc.
      )
   ),
   Value
),ThisRecord),Value)

```


Reductive Search\
For the Items property in the gallery:
```
Filter(
    Collection1,
    IsBlank(
        Find(
            "0",
            Concat(
                Filter(
                    Split(
                        SearchInput3.Text,
                        ";" //or any delimiter.
                    ),
                    !IsBlank(ThisRecord.Value)
                ),
                If(
                    TrimEnds(ThisRecord.Value) in Product || TrimEnds (ThisRecord.Value) in Color, // and more columns etc.
                    "1",
                    "0"
                )
            )
        )
    )
)
```


Wildcard * Character Search\
For the Items property in the gallery:
```
Switch(true,
And(
    IsBlank(Find("*",SearchInput2.Text)),
        !IsBlank(SearchInput2.Text)), Filter(Collection1,SearchInput2.Text in Product),  

IsBlank(SearchInput2.Text),Collection1, //if search is empty, display full collection
(Find("*",SearchInput2.Text) = 1),
    Filter(Collection1, Lower(Mid(SearchInput2.Text,2, Len(SearchInput2.Text)-1)) in Mid(Product,1,Len(SearchInput2.Text)-1)),
(Find("*",SearchInput2.Text) > 1),
    Filter(Collection1, Lower(Mid(SearchInput2.Text, 1,Len(SearchInput2.Text)-1)) in Lower(Mid(Product,Len(Product) - Find("*", SearchInput2.Text,1)+2,Len(SearchInput2.Text)-1))))
```
