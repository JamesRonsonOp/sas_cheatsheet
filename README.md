# sas_cheatsheet
snippets of sas code

[Penn State SAS tutorial and questions](https://online.stat.psu.edu/stat481/book/export/html/667)

## Iterative Do Loops
```
DO index-variable = start TO stop BY increment;
        action statements;
   END;
```

where:

DO, index-variable, start, TO, stop, and END are required in every iterative DO loop
index-variable, which stores the value of the current iteration of the DO loop, can be any valid SAS variable name. It is common, however, to use a single letter, with i and j being the most used.
start is the value of the index variable at which you want SAS to start the loop
stop is the value of the index variable at which you want SAS to stop the loop
increment is by how much you want SAS to change the index variable after each iteration. The most commonly used increment is 1. In fact, if you don't specify a BY clause, SAS uses the default increment of 1.

or example, this DO statement:

do jack = 1 to 5;
tells SAS to create an index variable called jack, start at 1, increment by 1, and end at 5, so that the values of jack from iteration to iteration are 1, 2, 3, 4, and 5. And, this DO statement:

do jill = 2 to 12 by 2;
tells SAS to create an index variable called jill, start at 2, increment by 2, and end at 12, so that the values of jill from iteration to iteration are 2, 4, 6, 8, 10, and 12.

#### Example: 

```
DATA multiply (drop = i);
    multiple = 0;
    do i = 1 to 20;
    	multiple + 5;
        output;
	end;
RUN;

PROC PRINT NOOBS;
	title 'Multiples of 5 up to 100';
RUN
```
* Pay attention to the Output statement. This is what outputs each iteration. 

In this case, we are not interested in one particular multiplication, but rather in a series of multiplications, 1 × 5, 2 × 5, 3 × 5, ... That's where the OUTPUT statement comes into play. The previous example created just one observation, because it relied on the automatic output at the end of the DATA step. Here, we override the automatic output by explicitly telling SAS to output the value of the multiple variable every time that SAS adds 5 to it. The DATA statement's DROP= option tells SAS not to bother to output the index variable i. Now, launch and run  the SAS program, and review the output from the PRINT procedure to convince yourself that our code properly generates the multiples of 5.

### Counting Backwards by 1

```
The following SAS program uses an iterative DO loop to count backwards by 1:

DATA backwardsbyone;
	do i = 20 to 1 by -1;
	    	output;
        end;
RUN;

PROC PRINT data = backwardsbyone NOOBS;
	title 'Counting Backwards by 1';
RUN;
```

As you can see in this DO statement, you can decrement a DO loop's index variable by specifying a negative value for the BY clause. Here, we tell SAS to start at 20, and decrease the index variable by 1, until it reaches 1. The OUTPUT statement tells SAS to output the value of the index variable i for each iteration of the DO loop. Launch and run   the SAS program, and review the output from the PRINT procedure to convince yourself that our code properly counts backwards from 20 to 1.



### Specifying a series of items

Rather than specifying start, stop and increment values in a DO statement, you can tell SAS how many times to execute a DO loop by listing items in a series. In this case, the general form of the iterative DO loop looks like this:

DO index-variable = value1, value2, value3, ...;
	action statements;
END;
where the values can be character or numeric. When the DO loop executes, it executes once for each item in the series. The index variable equals the value of the current item. You must use commas to separate items in a series. To list items in a series, you must specify

either all numeric values:
   DO i = 1, 2, 3, 4, 5;
all character values, with each value enclosed in quotation marks
   DO j = 'winter', 'spring', 'summer', 'fall';
or all variable names:
   DO k = first, second, third;

## Nesting Do Loops

8.2 - Nesting Do Loops
One way to make iterative DO loops even more powerful is to place one DO loop inside of another. Putting a DO loop within another DO loop is called nesting. We'll take a look at a few examples here.


# TEXT/STRING FUNCTIONS

### Length

* `LENGTH(string)` The LENGTH function returns a length in bytes. The KLENGTH function returns a length in a character-based unit.
* `LENGTHN(string)` The LENGTH and LENGTHN functions return the same value for non-blank character strings. LENGTH returns a value of 1 for blank character strings, whereas LENGTHN returns a value of 0.
* `LENGTHC(string)` The LENGTH function returns the length of a character string, excluding trailing blanks, whereas the LENGTHC function returns the length of a character string, including trailing blanks.
* `LENGTHM(string)` The LENGTH function returns the length of a character string, excluding trailing blanks, whereas the LENGTHM function returns the amount of memory in bytes that is allocated for a character string.

### Concatenation
**NOTE:** The CAT* functions and concatenation operator can combine character and numeric variables into a single (larger) character value.  The process implicitly converts a numeric value into a character and doesn't generate a SAS note or warning, unlike some of the other conversion methods.  (For example, when you assign a numeric value to a character variable.)  

* `||` Inline string concatenation operator. This concatenation operator is convenient, but doesn't provide the same flexibility as the CAT* functions to control how white space is trimmed.

* `CAT(item-1 <, …, item-n>)` Does not remove leading or trailing blanks and returns a concatenated character string. You can control how it handles white space though. 

* `CATS` The CATS function combines values by first removing any leading or trailing blank spaces, then returns the concatenated string.  For example: 
```
data report(keep=report);
 set sashelp.class;
 report = cats(name, ', Age:',age);
run;
```
OUTPUT: `Alfred, Age:14`

* `CATX`Use CATX function to create a character string that combines multiple values and separates them with a delimiter of one or more characters.  Like the CATS function, CATX trims leading and trailing blanks before combining the values.  For example:
```
data csv (keep=extract);
 set sashelp.class;
 extract = catx(',',name,age,weight,height);
run;
```
OUTPUT: `Alfred,14,112.5,69`

* Create a comma-seperated list of all variables. I take the value from each column and separate them by commas.
```data all (keep=full);
 set sashelp.class;
 full = catx(',',of name--weight);
run;
```
 
* Return only character variables separated by a special symbol. 
```
data char (keep=text);
 set sashelp.class;
 text = catx('|',of name-character-weight);
run;
```

### Align Text

`LEFT`
`RIGHT`

### Casing

`UPCASE`
`LOWCASE`

### Removing Characters

`TRIM`
`COMPRESS`

### Indexing

`INDEX` -Finds substrings
`SUBSTR` -Extracts substrings

### Splitting Strings

`SCAN`
