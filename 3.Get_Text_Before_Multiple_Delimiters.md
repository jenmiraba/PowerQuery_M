

# M - Get Text Before Multiple Delimiters

## Problem Description
In Power Query, it is often necessary to extract a substring from a text column based on a delimiter. To get the text before a single delimiter in a column, we can use the "Text.BeforeDelimiter" function with the interface. This function returns the substring of text that appears before the specified delimiter.

However, when there are multiple delimiters in the same column, things get a bit more complicated. In this case, you can use the "Text.PositionOfAny" function to find the position of any of the delimiters, and then use "Text.Start" to extract the text before the first occurrence of any of the delimiters.

![Alternate image text](https://i.imgur.com/uJo0n11.png)

## Purpose
This formula can be useful if you have a column with values that are in the format "Name & Surname" and you need to split these values into two separate columns, this formula can be used to extract the first part of the string ("Name") into a new column. Posible examples:

"John & Smith / Company" --> Clean text: "John"

"12-04-2023" --> Clean text: "12"

"Apple & Orange & Banana" --> Clean text: "Apple "

"1234-5678" --> Clean text: "1234"

"Jane Smith" --> Clean text: "Jane"


** There are other ways to achieve the same results, this is one apporach. **

### M Code - To Transform the Column

This formula transform the column where the values to be cleaned lie, and does not create a new column.

```
let
    
    Source = <your data source>,
    #"Cleaned Column" = Table.TransformColumns(Source, {{"ColumnName", each Text.Start(_, Text.PositionOfAny(_, {"&", "/", "-", " "})), type text}})

in  
    #"Cleaned Column"
```

### M Code - Add a New Column

```
let
    
    Source = <your data source>,
    #"Added Column" = Table.AddColumn(Source, "New Column Name", each Text.Start([ColumnName], Text.PositionOfAny([ColumnName], {"&", "/", "-", " "})), type text)

in  
    #"Added Column"
```

Notes:

- This formula assumes that the delimiter characters are &, /, - and space. They can be changed as needed by adjusting the formula.

- The type of the column to get the text from should be text, otherwise the formula will return an error.

## Authors

- [@jenmiraba](https://github.com/jenmiraba)


## Tech

**Power Query** 
Data transformation and cleansing tool built into Microsoft Excel and Power BI. It provides a graphical interface for creating and manipulating data transformations. 


**M Language**
Functional programming language used by Power Query to create custom data transformations. It is a powerful tool that allows for complex data manipulation, filtering, and aggregation.


