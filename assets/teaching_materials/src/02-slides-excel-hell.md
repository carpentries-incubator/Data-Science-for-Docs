---
title: "Excel Hell"
author: "Steve Harris"
institute: "The DataSciBC"
date: "2019/09/17 (updated: `r Sys.Date()`)"
output:
  xaringan::moon_reader:
    css: [default, metropolis, metropolis-fonts]
    lib_dir: libs
    nature:
      highlightStyle: github
      highlightLines: true
      countIncrementalSlides: false
---

# Excel Hell

<!-- create the html version using the pandoc command below -->
<!-- pandoc -t revealjs -s --slide-level=2 -V theme=solarized 02-lesson-02-excel-hell-slide.md -o 02-lesson-02-excel-hell-slide.html -->

## Learning Objectives 

1. Learn about data types (columns)
2. Spreadsheets <> Data (Rows <> Observations)
3. Best practices for recording data
4. Common mistakes

## Outline

- [Have a go](#have-a-go)
- [Data Types](#data-types)
- [Cardinal rules](#cardinal-rules)
- [Common mistakes](#common-mistakes)
- [Unravelling Data](#bad-data)
- [Exporting to CSV](#worked-example)
- [Testing your spreadsheet](#testing)
- [Have a go again](#have-a-go-again)

<a name="have-a-go"></a>

# Have a go ...

Please design an excel spreadsheet for a study of anaesthesia techniques on a labour ward. We're interested in the maternal and fetal outcomes and we'd like to record anaesthetic interventions.

## You must be able to record

- date and time of procedure
- anaesthetic technique  
- indication (LSCS, analgesia, PPH etc.)
- anaesthetist grade  
- maternal age  
- maternal parity  
- date and time of birth
- method of delivery (SVD, instrumental, LSCS)
- APGAR 

## Data entry

1. 23F primip having epidural for analgesia then singleton birth via SVD with APGAR 8 
2. Same woman having a twin birth via LSCS 3 years later: APGARS 7 for first, but not recorded for second twin
3. 32F multip having epidural for analgesia by labour ward anaesthetic reg then crash GA section by anaesthetic consultant for fetal distress with APGAR 3

## Review

<a name="data-types"></a>

# Data types

##

> If in doubt, aim for **consistency in every column**. Never try to record more than one "type" of thing in a column.

## Integers & Decimals

- `...,-3,-2,0,1,2,3,...` versus `3.141529`
- Integers are any whole number
- Decimals include any number with a decimal point

## Strings

> A string is any sequence of characters. 

- Literally anything you can type can be represented as a string. 
- Default type in Excel
- Be careful ` 180mg ` is not a number!

## Date/Time objects

- A number as far as the computer is concerned
- Often (but not always)
    - Dates are integers counted from 1 Jan 1970
    - Times are fractions of a day
- Other possibilities
    - milliseconds since 1960
    - Days since January 0 1900 (Excel!)

## Date gotcha's

![](img/excel-dates.png)

## Booleans

- `TRUE` or `FALSE` statements.
- `1` or `0` is a common shorthand

## Factors

- 'Categorical' (ordered or unordered)
- Integers with labels

## Nominal

- An **un**ordered (nominal) factor
- Named but not ordered

```
- apples
- oranges 
- pears
```

- R stores this as `1,2,3` for convenience<br/>but not because `1<2<3`.

## Ordinal

- An ordered (ordinal) factor such as a Likert scale
- Ordered and named

```
- Strongly disagree
- Disagree
- Neither agree/disagree
- Agree
- Strongly agree
```

- R stores this as `1,2,3,4,5` for convenience and understands that `1<2<3<4<5`

# Exploring Datatypes in R Studio

## Your turn ...

In R studio,

```R
integers <- as.integer(c(1, 3, 15, 16))
decimals <- c(1.4, 3.5, 15.55, 16.4)
bools <- c(T, T, F, T)
dates <- as.Date(c("22/04/2016", "13/05/1997"), format = "%d/%m/%Y")
strings <- c("These are", "Strings")
factors <- as.factor(c("Apples", "Pears", "Lemons"))
factors <- as.factor(c("Good", "Better", "Best"), ordered=TRUE)
```

then use `str()` to see the data 'structure'

<a name="cardinal-rules"></a>

# Cardinal rules

<!-- - [ ] TODO(2016-05-26): need to explain the 'header row' concept -->

The cardinal rules of using spreadsheet programs for data:

## Columns

> Put all your **variables in columns** - the thing you're measuring, like 'weight', 'temperature' or 'SBP'. Break things down into their most basic constituents, and keep units in your headers only.

## Rows

> Put each **observation in its own row**. Think very carefully about what constitutes your basic observation. Often it's your patient, but it may not be as intuitive as you think.

## Headers

> Have a single 'header' row to label your columns 

## Cells

> **Don't combine multiple pieces of information in one cell**.

> **Leave the raw data raw** - don't mess with it! That means no formulas anywhere in your spreadsheet!

## Sharing

> Export the cleaned data to a **text based format** like CSV. This ensures that anyone can use the data, and is the format required by most data repositories.

# Try to think like a computer  #

## The computer doesn't care about formatting

![](img/data2csv-3.png)

## We do ... 

![](img/data2csv-2.png)

just add some white space and dividers

## And Excel ...

And all excel does is present it to us in an easy to use format.

![](img/data2csv-1.png)

## But ...

> But you always need to remember that you need to go back and forth between both formats.

> So merged cells, colours, comments will both be lost and confuse.


# Your turn ...

## The data

- Raw data from an RCT on pain relief following mastectomy
- Download from [FigShare](https://figshare.com/s/165cad3ce6eadbf6b19a).

## Original (dirty)

![](img/excel1.png)

## Your mission ...

Identify and fix these common mistakes

<a name="common-mistakes"></a>

# Common mistakes

<!-- - [ ] TODO(2016-05-26): this would work nicely as a round robin teaching exercise; get each pair to read one section and teach the rest of the glass; repeat twice if needed to get through the whole list -->

- [Multiple tables](02-lesson-02-excel-hell.html#tables)
- [Multiple tabs](02-lesson-02-excel-hell.html#tabs)
- [Not filling in zeros](02-lesson-02-excel-hell.html#zeros)
- [Using bad null values](02-lesson-02-excel-hell.html#null)
- [Using formatting to convey information](02-lesson-02-excel-hell.html#formatting)
- [Using formatting to make the data sheet look pretty](02-lesson-02-excel-hell.html#formatting_pretty)
- [Placing comments or units in cells](02-lesson-02-excel-hell.html#units)
- [More than one piece of information in a cell](02-lesson-02-excel-hell.html#info)
- [Field name problems](02-lesson-02-excel-hell.html#field_name)
- [Special characters in data](02-lesson-02-excel-hell.html#special)
- [Inclusion of metadata in data table](02-lesson-02-excel-hell.html#metadata)
- [Date formatting]()


<a name="tables"></a>

## Multiple tables

A common strategy is creating multiple data tables within one spreadsheet. **This confuses the computer, so don't do this!**. When you create multiple tables within one spreadsheet, you're drawing false associations between things for the computer, which sees each row as an observation. You're also potentially using the same field name in multiple places, which will make it harder to clean your data up into a usable form.

<a name="tabs"></a>

## Multiple tabs

1. More likely to accidentally add inconsistencies to your data 
2. You add an extra step for yourself before you analyze the data because you will have to combine these data into a single datatable.

## Multiple tabs: An exception ... 

- readme
- data dictionary
- raw data

<a name="zeroes"></a>

## Not filling in zeroes

It might be that when you're measuring something, it's usually a zero, say the number of times an elephant is observed in the object or the survey. Why bother writing in the number zero in that column, when it's mostly zeros?

<a name="null"></a>

## Using bad null values

**Example**: using -999 or other numerical values (or zero).

**Solution**: Many statistical programs will not recognize that numeric values of null are indeed null. It will depend on the final application of your data and how you intend to analyse it, but it is essential to use a clearly defined and CONSISTENT null indicator. Blanks (most applications) and NA (for R) are good choices.

<a name="formatting"></a>

## Using formatting to convey information 

**Example**: highlighting cells, rows or columns that should be excluded from an analysis, leaving blank rows to indicate separations in data.

**Solution**: Computers are colour blind. Colour coding if fine if it helps you understand your data, as long as you recognise that it won't have any value in R. Adding in extra rows or columns to help format your data is going to damage your data as it will be interpreted as new observations. Create a new field to encode which data should be excluded.

<a name="formatting_pretty"></a>

## Using formatting to make the data sheet look pretty

**Example**: merging cells.

**Solution**: If you're not careful, formatting a worksheet to be more aesthetically pleasing can compromise your computer's ability to see associations in the data. Merged cells are an absolute formatting NO-NO if you want to make your data readable by statistics software. Consider restructuring your data in such a way that you will not need to merge cells to organize your data. If you have a number of column headings under the same umbrella term, consider just adding a prefix to each header instead.

<a name="formatting"></a>

## Placing comments or units in cells

**Example**: You want to leave yourself a comment to identify bad data, or explain away an outlier.

**Solution**: Most statistical programs can't see Excel's comments, and would be confused by comments placed within your data cells. As described above for formatting, create another field if you need to add notes to cells. Similarly, don't include units in cells: ideally, all the measurements you place in one column should be in the same unit, but if for some reason they aren't, create another field and specify the units the cell is in.

<a name="units"></a>

## More than one piece of information in a cell

**Example**: You are taking serial BP measurements. You record this as 180/80, 175/76, 168/82

**Solution**: Never include more than one piece of information in a cell. If you need all these measurements, design your data sheet to include this information in separate columns. In fact, in the above example, it would even be beneficial to separate out each systolic and diastolic value. You final column heading might look like this: sbp_1, dbp1, sbp_2, dbp_2, sbp_3, dbp_3.

<a name="field_name"></a>

## Field name problems

Choose descriptive field names, but be careful not to include: spaces, numbers, or special characters of any kind. Spaces can be misinterpreted by parsers that use whitespace as delimiters and some programs don't like field names that are text strings that start with numbers.
Underscores (`_`) are a good alternative to spaces and consider writing names in camel-case to improve readability. Remember that abbreviations that make sense at the moment may not be so obvious in 6 months but don't overdo it with names that are eccessivly long.

## Examples

**good name** | **good alternative** | **avoid**
------------- | -------------------- | ---------
Max_temp | MaxTemp | Maximum Temp (°C)
Precipitation | Precipitation_mm | precmm
Mean_year_growth | MeanYearGrowth | Mean growth/year
sex | sex | M/F
weight | weight | w.
cell_type | CellType | Cell type
first_observation | Observation_01 | 1st Obs.

<a name="special"></a>

## Special characters in data

**Example**: You treat Excel as a word processor when writing notes, even copying data directly from Word or other applications.

**Solution**: This is a common strategy. For example, when writing longer text in a cell, people often include line breaks, em-dashes, et al in their spreadsheet.  Worse yet, when copying data in from applications such as Word, formatting and fancy non-standard characters (such as left- and right-aligned quotation marks) are included.  When exporting this data into a coding/statistical environment or into a relational database, dangerous things may occur, such as lines being cut in half and encoding errors being thrown.

General best practice is to avoid adding characters such as newlines, tabs, and vertical tabs. In other words, treat a text cell as if it were a simple web form that can only contain text and spaces.

<a name="metadata"></a>

## Inclusion of metadata in data table

**Example**: You add a legend at the top or bottom of your data table explaining column meaning, units, exceptions, etc.

**Solution**: While recording data about your data ("metadata") is essential, this information should not be contained in the data file itself. Unlike a table in a paper or a supplemental file, metadata (in the form of legends) should not be included in a data file since this information is not data, and including it can disrupt how computer programs interpret your data file. Rather, metadata should be stored as a separate file in the same directory as your data file, preferably in plain text format with a name that clearly associates it with your data file. Because metadata files are free text format, they also allow you to encode comments, units, information about how null values are encoded, etc. that are important to document but can disrupt the formatting of your data file.


<a name="worked-example"></a>

# Tips

##

- 3 sheets: readme, dictionary, data ... then export,share the data sheet
- Data validation in Excel
- Learn to export to CSV




