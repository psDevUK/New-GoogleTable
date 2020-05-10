# New-GoogleTable
A Google Table for UniversalDashboard based on https://www.npmjs.com/package/react-google-charts

## As Always Please Support the Developer and buy the Enterprise license

## Google Table

**New-GoogleTable** is the name for this component and it does come in various formats on the developer site, but the bar chart
in a table format I saw the best display of chart as you can already place icons in a table in UniversalDashbaord.  So I wanted
to be able to produce a component that didn't already exist in UniversalDashboard.

## How To Use
  I should do more testing on the components I put together, but as long as they work and display the data provided then in my book
  that is a pass, then I look to build the next component.  So whilst proving this component does work I did find it to be a bit
  **picky** on how the data is provided.  So please remember that when using this component, it is **picky** on how the data is 
  provided.
  
## Parameters
    **-Data** supplied in a two dimensional array that has a header and must make sure the number is an integer (see demo)
    **-Width** defines the width of the table to be displayed defaulted to 500px
    **-Height** defines the height of the table to be displayed defaulted to 500px
    **-ColumnWidth** allows you to change the column width to display more data defaulted to 120
    **-RowNumber** boolean value to decide if row numbers should be shown, defaulted to $true
    **-FirstRow** decides the first row of data to be displayed from the array passed, defaulted to 1
    **-FrozenColumn** integer to decide if a certain column is frozen RowNumner has to be true and paging off
    **-Paging** validateset for paging defaulted to disabled
    **-TableRows** decides the amount of rows per table, only active is paging is on
    **-SortAscending** boolean value to decide if it should be sorted ascending defaulted to true
    **-SortColumn** decides which column to sort the data on (see demo)
    
  ## Demonstration Of The Component
  This should be a generic tast file that should work on anyones windows-based computer...
  
  ```
Import-Module -Name UniversalDashboard
Import-Module -Name UniversalDashboard.GoogleTable
Get-UDDashboard | Stop-UDDashboard
Start-UDDashboard -Port 10005 -Dashboard (
    New-UDDashboard -Title "Powershell UniversalDashboard" -Content {
        New-UDHeading -Size 3 -Text "New-GoogleTable"
        $MultiArray = @()
        Get-Process | Sort-Object -Unique Name | Select-Object Name, @{Label = "Handles"; Expression = { [math]::Round($_.Handles, 1) } } | Export-Csv C:\UD\Test.csv -NoTypeInformation
        $MultiArray += , @('Name', 'Handles')
        import-csv "C:\UD\Test.csv" | % { $MultiArray += (, ($_.Name, [int]$_.Handles)) }
        New-GoogleTable -Id "TABLECHART" -data @($MultiArray) -Width "500px" -Height "500px" -RowNumber $false -ColumnWidth 200 -SortAscending $false -FrozenColumn 1 -FirstRow 2 -SortColumn 1
    }
)

  ```
  
