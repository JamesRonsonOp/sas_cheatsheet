
COMBINE TABLES WITH SAS LANGUAGE
/* Perform and analyze Annual Revenue 


THIS STEP WAS ONLY NECESSARY FOR THE EXCERCISE I WAS DOING
-combine 4 tables */

PROC IMPORT DATAFILE='/home/u59013950/udemy1/sales1.xlsx' DBMS=XLSX OUT=sales_spring;
SHEET='spring';
GETNAMES=YES;

PROC IMPORT DATAFILE='/home/u59013950/udemy1/sales1.xlsx' DBMS=XLSX OUT=sales_summer;
SHEET='summer';
GETNAMES=YES;

PROC IMPORT DATAFILE='/home/u59013950/udemy1/sales1.xlsx' DBMS=XLSX OUT=sales_autumn;
SHEET='autumn';
GETNAMES=YES;

PROC IMPORT DATAFILE='/home/u59013950/udemy1/sales1.xlsx' DBMS=XLSX OUT=sales_winter;
SHEET='winter';
GETNAMES=YES;

/* THIS IS HOW YOU ACTUALLY COMBINE TABLES

STEP 1: Create a new table. Here it is called annual
DATA annual;
STEP 2: Select tables you would like to combine. 
SET spring summer autumn winter;
STEP 3: RUN;
*/

DATA annual;
SET WORK.sales_spring WORK.sales_summer WORK.sales_autumn WORK.sales_winter;
RUN;

PROC IMPORT OUT=UDEMY1.purchase DATAFILE='/home/u59013950/udemy1/SQL - purchases.csv'
DBMS=CSV REPLACE; GETNAMES = YES;
RUN;

PROC IMPORT OUT=UDEMY1.item DATAFILE='/home/u59013950/udemy1/SQL - items.csv'
DBMS=CSV REPLACE; GETNAMES = YES;
RUN;

PROC IMPORT OUT=UDEMY1.customer DATAFILE='/home/u59013950/udemy1/SQL - customers.csv'
DBMS=CSV REPLACE; GETNAMES = YES;
RUN;

proc sql;

SELECT * FROM UDEMY1.purchase
INNER JOIN ;

quit;


_______________
### Creating Datasets with SAS Language ###

/* ### Creating a dataset as strings ### */

DATA sample; /* create data set name it sample. */
INPUT height weight; /* create two variables height and weight */
DATALINES; /* this command tells SAS that we are going to input data */
170 300 
131 192
231 421
; 

RUN;

proc print data=sample;run; /* print results into a results window */


/* ### Creating a dataset with a variable that is a string/char ### */

DATA sample; 
INPUT height weight name $; /* The $ after name indicates it is a character variable */
DATALINES;
170 300 Joe
131 192 Alice
231 421 Roma
;
RUN;

proc print data = sample;run;

__________
/* EXPORT TO CSV */

PROC EXPORT DATA=import OUTFILE='/Users/jamesopacich/Documents/udemy_SAS_1/datasets/export.csv' 
DBMS=CSV;
RUN;

/* TO EXPORT TO TEXT FILE change the .csv to .txt in the file path and then change the dbms to TAB

DMBS=TAB;

_________

/* Filtering through records in a table */

/*
DATA name_of_new_dataset;
SET  table;
IF condition;
RUN;
*/

/* EXAMPLE */

DATA homerun_leaders;
SET SASHELP.BASEBALL;
IF CrHome > 20;
RUN;

_______________
/* ---THIS SNIPPET INCLUDES THE FOLLOWING--- 

1. Import Text File
2. Import Excel File
3. Import CSV File
	* Including ways to specify datatypes for each column/variable
	* Including INFILE parameters like delimiter,missover and first obs. 
------------------------------------------------------------------------

____________________________
/* ### IMPORT TEXT FILE ###
___________________________
*/

data student2; /* Naming The SAS table */
INFILE '/home/u59013950/sasuser.v94/studenttest.txt';
INPUT name $ age grade; /* Naming columns. Not sure what $ does */
RUN;

_____________________________________________
/* ### IMPORT EXCEL FILE with PROC IMPORT ### 
_____________________________________________
*/

/* ---PROC IMPORT Parameters---

1. File path 													DATAFILE =
2. Format (DBMS) 												DBSM =
3. Output or Destination Name (You Specify This) 				OUT = 
4. Name of Worksheet (On the tab of the excel worksheet) 		SHEET = 
5. Get Names (Grabs Column Headers from 1st Row) 				GETNAMES = 
*/

PROC IMPORT DATAFILE='C:\' DBMS=XLSX OUT=name_of_destination;
SHEET='name_of_sheet';
GETNAMES=YES;




/* ### IMPORT CSV FILE ### 
____________________________ 
*/

/* ## Benefit of CSV vs EXCEL ##

-- Specify Data Format/Types When Importing

  --- DATA parameters---
  
  1. Specify Name for Data set 					DATA name_of_project;
  2. Specify Path for CSV and INFILE hyperparameters
  												INFILE 'C:\' DSD MISSOVER FIRSTOBS=2;
  3. Identify datatypes with INPUT				INPUT CUSIP$ fyear name$; 
  4. RUN
  
  ## NOTE on INFILE parameters
  --DSD (delimiter-sensitive data): It recognizes two consecutive delimiters as a
  missing value; it allows you to include delimiters within quoted strings. 
  --MISSOVER: This option prevents SAS from going to a new input line if it does
  not find values for all of the variables(columns) in the current line of data, 
  so you don't get messy results. 
  --FIRSTOBS: This option tells SAS on what line you want it to start reading your
  raw data file. 
  
  ## NOTE ON DENOTING DATATYPES
  --String format gets $ at end of column name. for example: column_name$
  --number format gets nothing at the end of the column.: column_name
______________
/* Print the last modified data table */

PROC PRINT;
RUN;

/* Print a specific table */

PROC PRINT DATA=name_table;
RUN;
______________
/* SORTING */ 

/*

STEP 1: PROC SORT statement
STEP 2: indicate which table you want to sort with DATA=table
STEP 3: indicate name of the result table with OUT=new_table_name
STEP 4: Close that line with semi-colon
STEP 5: BY statement
STEP 6: indicate column you are storing by
STEP 7: End that line with semi-colon
STEP 8: RUN statement end with semi-colon

PROC SORT DATA=table OUT=new_table_name;  
BY column;
RUN;
*/

/* SORT ASCENDING */

PROC SORT DATA=SASHELP.BASEBALL OUT=homeruns;
BY CrHome;
RUN;

/* SORT DESCENDING */
PROC SORT DATA=SASHELP.BASEBALL OUT=homeruns;
BY DESCENDING CrHome;
RUN;


___________________
/* ### IDENTIFYING COLUMN NAMES AN DTYPES ### */


/* using SAS contents clause to get table info */
proc contents data=udemy1.purchase;
run;

/* using proc sql to get table info */
proc sql;
select * from dictionary.columns
where libname = 'UDEMY1' and memname = 'PURCHASE'
;
quit;

/* Using SAS vcolumn view */

data columns;
set sashelp.vcolumn;
where libname = 'UDEMY1' and memname = 'PURCHASE';
run;
_______________
/* ### CONTENT REPORTS AND SUMMARY STATISTICS ### */

/* THIS IMPORTS PRACTICE DATASET */

PROC IMPORT OUT=comp DATAFILE='/home/u59013950/sasuser.v94/sp500.csv' DBMS = CSV;
GETNAMES=YES;
RUN;

/* ----------------------------------------- */

/* ### CREATING A DATA CONTENTS REPORT ### */

/* comp is the name of the table */

PROC CONTENTS DATA=comp;run;


/* ### SUMMARY STATISTICS FOR WHOLE TABLE ### */

PROC MEANS DATA=comp;RUN;


/* ### SUMMARY STATISTICS FOR JUST ONE VARIABLE ### */

PROC MEANS DATA=comp;
VAR HIGH;
RUN; 

/* ### SUMMARY STATISTICS WITH TAIL DISTRIBUTIONS ### */

PROC MEANS DATA=comp MEAN mEDIAN STD P5 P95 MIN MAX;
VAR HIGH;
RUN;
_____________
/* Data Steps v. Proc Steps */

/* DATA STEPS

- Begin with DATA statement
- read and modify data
- create a SAS data set

PROC STEPS

- Begin with PROC statements
- Perform specific analysis or function
- produce results or report
________________
/* ### REPLACEMENT FOR LIMIT CLAUSE IN PROC SQL ### */

/* You can limit the number of rows processed and returned by using the INOBS= and OUTOBS= options in PROC SQL.

 

INOBS= restricts the number of rows that PROC SQL retrieves from any single data source.

OUTOBS= restricts the number of rows that PROC SQL includes in the output.

 

So if you want to consider all rows in your query but limit the number returned, use OUTOBS=.

 

If the source table is SAS then I would use a data step.  Examples follow. */


proc sql outobs=1;
  select *
  from UDEMY1.purchase;
quit;

proc sql inobs=1;
	select * 
	from udemy1.purchase;
quit;
_________________

/* Linear Regression */ 

/* ---SIMPLE LINEAR REGRESSION---

1. PROC REG clause
2. DATA=name_of_table
3. ;
4. MODEL column_1=column_2
5. ;
6. RUN ;
7. Use R-squared as main measure of model accuracy

*/

PROC REG DATA=IMPORT;
MODEL rent=year;
RUN;

/* ---Regression Options---

1. Residual Value
2. Predicted Value

1. Add new line below Model command
2. OUTPUT clause 
3. OUT=res ---Outputting to a new dataset called res 
4. RESIDUAL=resid ---store residual to new variable called resid
5. P=pred ---store predicted value to a new variable called pred
6. ;
7. RUN;
8. NOTE: you must print the result to see it. 
9. PROC PRINT DATA=res; RUN;

*/

PROC REG DATA=IMPORT;
MODEL rent=year;
OUTPUT OUT=res RESIDUAL=resid P=pred;
RUN;

PROC PRINT DATA=res;RUN;

/* ---MULTIPLE LINEAR REGRESSION---

1. After MODEL clause you will add more variables
2. Use Adjusted R-squared as main metric for model accuracy

*/

PROC REG DATA=SASHELP.BASEBALL;
MODEL Salary=nHits nHome YrMajor;
OUTPUT OUT=res RESIDUAL=resid P=pred;
RUN;

PROC PRINT DATA=res;RUN;


/* ---Making Predictions--- */

/* 

Step 1. Create New Dataset 

-The periods represent empty spaces where our predictions will go

*/
DATA new;
INPUT rental_rates age operating_expenses vacancy_rates SQfootage;
DATALINES;
. 4 10 0.1 80000
. 6 11.5 0 12000
. 12 12.5 .32 340000
; 
RUN;

/* Step 2. combine datasets */

DATA combined_rent;
SET commrent new;
RUN;

/* Step 3. Make predictions

-predictions will automatically be made in this case
-the backslash starts the ability to list regression options.
-The only regression option chosen here is CLI.
-CLI is the confidence interval option that report upper and lower CIs 
-When this is a run a report will show in results and the missing values will be predicted in a different row.*/

PROC REG DATA=combined_rent;
MODEL rental_rates = age operating_expenses vacancy_rates SQfootage / CLI;
RUN;

/* ---FEATURE SELECTION--- */

/* Step 1. View results of regression with all variables

-analyze the p-values. Any that are above .05 should be considered
possible variables/features that are not relevant. 

*/

PROC REG DATA=commrent;
MODEL rental_rates = age operating_expenses SQfootage vacancy_rates;
RUN;

/* STEP 2: Create and Test Null Hypothesis.

-In this case, vacancy_rate has a p value of .57 which indicates that is has a 
57 percent chance of being wrong. 
-The null hypothesis is that Vacancy rate is irrelevant
-Alternative hypothesis is that vacancy rate is relevant
H0:Vacancy rate is irrelevant
Ha: Vacancy rate is relevant
-The results for this test will show up below the graphs at the very bottom.
*/

PROC REG DATA=commrent;
MODEL rental_rates = age operating_expenses SQfootage vacancy_rates;
Vacancy: TEST vacancy_rates=0; /* This tests the variable */
RUN;

/* STEP 3: Eliminate the feature */
PROC REG DATA=commrent;
MODEL rental_rates = age operating_expenses SQfootage;
RUN;

/* STEP 4: record the model */

/* 
rental rate = 12.37 - .14 * Age + .26 * Expenses + 0.000008 * Square Footage

-Our model is significant at a 1% level. It explains 56.6% of the data. 

-According to the model, given other variables fixed, for each year a house ages, the rental rate
will decrease by .14 percent on average. 

For each unit expenses grows, the rental rate will increase by .24 percent on average. 

For each quare a house has, the rental rate will increase by 0.000008 percent on average. 

*/

/* STEP 5: Produce Graph of Predicted Value vs Real Value */
______________
PROC SQL 

PROC SQL;

	CREATE TABLE WORK.QUERY

	AS

	SELECT * FROM SASHELP.CARS;

RUN;
QUIT;

PROC PRINT DATA=WORK.QUERY; RUN;
__________
SAS MACRO

%MACRO printTable(table);

PROC PRINT DATA=&TABLE;RUN;

%MEND;

%printTable(SASHELP.CARS);

_________

/*----------------------------------------------*/
  /*      Macro Variables                        */
  /*----------------------------------------------*/

/* User Defined Global Variables */
%let city=Dallas;
%let date=25APR2014;
%let amount=343;

/* User Defined Local Variables */
%macro lvars;
   %local name day;
   %let name=Ed Norton;
   %let day=Friday;
   %put _local_;
%mend;

/* When we run this we will see the Local Variables in %lvar */
%lvars

/* This shows all global user and automatic macro variables */
%put _all_;
___________________

/*----------------------------------------------*/
 /*       %DO  statement                         */
 /*----------------------------------------------*/

 %macro shownote(length);
    %if &length = LONG %then %do;
       %put NOTE: This is a longer note.;
       %put NOTE: It is shown if the macro parameter is set to the value LONG.;
       %put NOTE: The default note is much shorter.;
    %end;
    %else %put NOTE: This is a short note;
%mend shownote;

%shownote(LONG)

  /* results should be:
  
 NOTE: This is a longer note.
 NOTE: It is shown if the macro parameter is set to the value LONG.
 NOTE: The default note is much shorter.
 
 */
 ___________
 %macro testif;
      %local x y z;
      %let x=10;
      %let y=5;
      %let z=0;
      %if &x > &y %then %put test 1 successful;
      %else %put test 1 failed;
      %if &x < &y %then %put test 2 failed;
      %else %put test 2 successful;
      %if &x %then %put test 3 successful;
      %else %put test 3 failed;
      %if &z %then %put test 4 failed;
      %else %put test 4 successful;
   %mend testif;

   %testif

  /* results should be:
test 1 successful
test 2 successful
test 3 successful
test 4 successful
*/
______________________
/*----------------------------------------------*/
  /*       Macro Parameters                       */
  /*----------------------------------------------*/


/* Positional Parameters */

%macro pospar(var1,var2,var3,var4,var5);
      %put &var1 &var2 &var3 &var4 &var5;
  %mend pospar;

  %pospar();

  /* results should be: *blank*  */


  %pospar(str1,str2,str3,str4,str5)


  /*  results should be: str1 str2 str3 str4 str5  */

  %pospar(str1)

  /* results should be: str1  */


/* Keyword Parameters  */

  %macro keypar(var1=str1,var2=str2,var3=);
  %put &var1 &var2 &var3;
  %mend keypar;

  %keypar();

  /* results should be: str1 str2  */


  %keypar();

  /* results should be: str1 str2  */

  %keypar(var1=abc,var2=def,var3=ghi)

  /* results should be: abc def ghi */

______________

  /*----------------------------------------------*/
  /*       Macro Quoting                          */
  /*----------------------------------------------*/


  %macro m;
    %put this is macro m;
  %mend m;

  %let p=%str(proc print; run;);
  %put p = &p;

  /* results should be:  p = proc print; run; */


  %let m=%nrstr(look at macro %m and var &m);
  %put m = &m;

  /* results should be: m = look at macro %m and var &m */


 data test;
    store="Tom's place";
    call symput('s',store);
run;

%macro test;
   %if %bquote(&s) ne %then %put *** valid ***;
   %else %put *** null value ***;
%mend test;
%test;

 /* results should be:  *** valid *** */


 %let bqtvar=%str(macro%'s here!);
     %put bqtvar = &bqtvar;

  /* results should be: bqtvar = macro's here! */


 %let nbqtvar=%nrstr(macro%'s and &procs);
 %put nbqtvar = &nbqtvar;

  /*---------------------------
   results should be:
      nbqtvar = macro's and &procs
   ---------------------------*/


  %put superqed variable = %superq(nbqtvar);

  /* results should be:  superqed variable = macro's and &procs */


  %let qsc=%qscan(&nbqtvar,1);
  %put qsc = &qsc;

  /* results should be: qsc = macro's  */


  %let qsu=%qsubstr(&nbqtvar,1,7);
  %put qsu = &qsu;

  /* results should be: qsu = macro's */


  %let qsp=%qupcase(&nbqtvar);
  %put qsp = &qsp;

  /* results should be:  qsp = MACRO'S AND &PROCS */


  %let mvar=%nrstr(%m);
  %put mvar = %unquote(&mvar);

  /*---------------------------
    results should be:
this is macro m
mvar =
   ---------------------------*/
   
   _____________
   /*----------------------------------------------*/
  /*       Macro Char Functions                   */
  /*----------------------------------------------*/


  /*------------------------------*/
  /*       %EVAL FUNCTION         */
  /*------------------------------*/

  %let num1=%eval(32767+7233);
  %put &num1 should be 40000;


  /*------------------------------*/
  /*       %INDEX FUNCTION        */
  /*------------------------------*/

  %let a=a very long value;
  %let b=%index(&a,v);
  %put v appears at position &b..;         /* at 3 */

  /*------------------------------*/
  /*       %LENGTH FUNCTION       */
  /*------------------------------*/

  %macro aproc;
     proc print; run;
  %mend aproc;

  %put %length(&a) should be 17;

  %put %length(%aproc) should be 16;

  /*------------------------------*/
  /*       %SCAN FUNCTION         */
  /*------------------------------*/

	%LET P=CATS AND DOGS;
	%LET Q=%SCAN(&P,3,%str( ));
	%put &q SHOULD BE DOGS;


  /*-------------------------------*/
  /*      %substr function         */
  /*-------------------------------*/

   %LET FIRST=THIS BOOK;
   %LET SECOND=%SUBSTR(&FIRST,6,4);
   %put &second SHOULD BE BOOK;


  /*-------------------------------*/
  /*      %UPCASE function         */
  /*-------------------------------*/

  %let string=%upcase(a string to upcase);
  %put &string should be A STRING TO UPCASE;
  
  
