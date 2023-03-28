
# M - Remove last N rows if condition is met

This repository contains an M Language Power Query script that can be used to remove the last rows of a table if a specified condition is met. The condition could be based for example on the presence of a specific word in a chosen column of the table, lenght of text or specific digits.

![Alternate image text](https://i.imgur.com/9tnxPKo.png)

## Purpose
The purpose of this script is to easily remove rows from the end of a table if they do not meet a specific criteria. This can be useful when working with large datasets where the last few rows do not contain relevant data, we don't know exactly how many rows have to be removed or if that number could change in the future.

## Notes
Please note that the code includes some examples of possible conditions, you may need to modify the script to suit your specific requirements.




# Usage/Examples

To use this script, follow these steps:

1. Open Power Query and load the table you want to remove the last N rows.
2. Click on the "Advanced Editor" button in the "View" tab of the ribbon.
3. Copy and paste the code below into the editor.
4. Uncomment the lines of the condition you need and/or adjust it to the one you want to search for. 
5. Click the "Done" button to close the editor.
6. Click "Close & Load" in the "Home" tab of the ribbon to apply the changes to the table.


## M Code

```let
    Source = GoogleSheets.Contents(MyWorksheet),

    // Get the row position where a condition of interest is met that will be removed along with all the rows after
    // Uncomment according to the condition needed

    // Example 1: Looking for a specific word or string like "ABC"
    // varPosition = List.PositionOf(Source[columnToSearch], "ABC"), 

    // Example 2: Looking for the first position of two or more specific words or strings like "ABC", "FGE"
    // varPosition = List.PositionOfAny(Source[columnToSearch], {"ABC", "FGE"}),

    // Example 3: Certain text length such as 3
    // varPosition = List.PositionOf(List.Transform(Source[columnToSearch], each Text.Length(_)), 3),

    // Example 4: Check for more than one length (4 and 7)
    // varPosition = List.PositionOfAny(List.Transform(Source[columnToSearch], each Text.Length(_)), {4, 7}),

    // Example 5: A specific number like 4
    // varPosition = List.PositionOf(Source[columnToSearch], 4),

    // Get total rows in the table //
    varTotalRows = Table.RowCount(Source),

    // Remove Last Rows //
    #"Remove Last Rows" = Table.RemoveLastN(Source, varTotalRows - varPosition)

in  
    #"Remove Last Rows"
```


## Authors

- [@jenmiraba](https://github.com/jenmiraba)


## Tech

**Power Query** 

**M Language**

