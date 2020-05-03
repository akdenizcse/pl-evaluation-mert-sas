# SAS(Statistical Analysis System)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/10/SAS_logo_horiz.svg/1280px-SAS_logo_horiz.svg.png)

SAS is a programming language, created to make analysis of variance and regression and designed to run on IBM System/360 computers. Initial intention was to use the language in agricultural analysis. 10 years later, after software handed to SAS Institute it becomes more statistical language in years.  Language was developed by Anthony James Barr at North Carolina State University in 1966 using C. 
  
SAS is designed for data access, manipulation, transformation and analysis. SAS has been using for data management, business intelligence, Predictive Analysis, Descriptive and Prescriptive Analysis etc. 

Over the years SAS added numerous solutions in its palette. It has solution for Data Governance, Data Quality, Big Data Analytics, Text Mining, Health science an many more.
     
SAS has more than 200 components. Some of them:
-	Base SAS – Basic procedures and data management
-	SAS/STAT – Statistical analysis
-	SAS/GRAPH – Graphics and presentation
-	SAS/OR – Operations research
-	SAS/ETS – Econometrics and Time Series Analysis
-	SAS/IML – Interactive matrix language
-	SAS/AF – Applications facility
-	SAS/QC – Quality control
-	SAS/INSIGHT – Data mining
-	SAS/PH – Clinical trial analysis
-	Enterprise Miner – data mining
-	Enterprise Guide - GUI based code editor & project manager
-	SAS EBI - Suite of Business Intelligence Applications
-	SAS Grid Manager - Manager of SAS grid computing environment [Source](https://en.wikipedia.org/wiki/SAS_(software) )

## Use cases
-	Data Management
-	Statistical Analysis
-	Quality Improvement
-	Data Extraction
-	Data Transformation

## Advantages of SAS
1.	SAS is a 4th generation language which makes it learn and debug easily.
2.	SAS provides Graphical User Interface for users who does not have programming knowledge.
3.	SAS has a strong ability to handle large datasets very easily.
4.	Ease of reaching to technical support

## Disadvantages of SAS
Since SAS is not an open source programming language, The most obvious disadvantage of SAS is cost. You have to buy different component to execute different tasks. This makes cost grow faster

## Book Recommendations to Learn SAS
- SAS Certification Prep Guide: Base Programming for SAS 9 by SAS Institute, 2015 [Link](https://www.amazon.com/SAS-Certification-Prep-Guide-Programming/dp/1607649241)
- Learning SAS by Example: A Programmer's Guide by Ron Cody, 2007 [Link](https://www.amazon.com/Learning-SAS-Example-Programmers-Second-ebook/dp/B07FN2WTHT)
- Learning SAS in the Computer Lab by Rebecca J. Elliott, 1995 [Link](https://www.amazon.com/Learning-SAS-Computer-Advanced-Cengage/dp/0495559687)

## Windows installation for SAS 9.4
-	SAS 9.4 is supported on Windows 7, 8, 8.1 or 10 
-	Since SAS is not an open source software, you must buy a licence key to install
- If you are modifying an existing a SAS deployment, perform a back up to SASHOME directory.
-	To install SAS software, use the SAS Deployment Wizard in your SAS Software Depot
    - Use the method appropriate for the host where software will be installed. Double click the setup.exe at the root of your SAS Software Depot to start SAS Deployment Wizard or right click to setup.exe and click run as administrator.
    
## Linux İnstallation for SAS 9.4
- SAS 9.4 is supported only on Red Hat Enterprise Linux 6 update 1, Oracle Linux 6.1, SuSE Linux Enterprise Server 11 SP1. For other Linux implementations, SAS may not install at all, or may install but not run.
-	Since SAS is not an open source software, you must buy a licence key to install
-	You must install under a user account with a umask 022. The root account should not be used. 
- Download and extract the software installation file using a SAS user account. The extracted folder is your SAS Software Depot
-	Using SAS user account, run setup.sh from SAS Software Depot
    - `$HOME/<SASDepot>/setup.sh`
    -	During installation you will have to specify SAS Home.
    -	SAS Foundation is the only product you must install. Other components are optional
-	Add the SASROOT directory to each user’s search path
    - `PATH=$PATH:<SASHOME>/SASFoundation/9.4`
## Mac installation for SAS 9.4
-	Currently there is not a version of SAS available for the Mac OS X operating system. However users can install VirtualBox on their mac and apply installation guide for Linux or Windows distribution.

# SAS Programming

SAS has 2 main parts; DATA steps and PROC steps

DATA steps typically create or manipulate datasets but also can be used to produce custom-designed reports
-	Putting data into a SAS dataset
-	Compute values for new variables
-	Check for to correct errors
-	Produce new SAS datasets

PROC steps typically for analysing and processing data. Proc steps control a library of prewritten routines that perform tasks on SAS datasets(i.e. listing, sorting, summarizing etc.)
-	Print a report
-	Produce descriptive statistics
-	Create a tabular report
-	Produce plots and charts

## Code Examples
- ***To create a table and print:***
```	
DATA LISTINP;
 INPUT ID HEIGHT WEIGHT GENDER $ AGE;
DATALINES;
 1 68 144 M 23
 2 78 202 M 34
 3 62 99 F 37
 4 61 101 F 45
 ;

PROC PRINT;
 TITLE 'Example 1';
RUN;
```

- ***To create a plot from custom table:***
```
DATA CRACK;
  INPUT ID AGE LOAD AGEF;
DATALINES;
  1  20 11.45 20
  2  20 10.42 20
  3  20 11.14 20
  4  25 10.84 25
  5  25 11.17 25
  6  25 10.54 25
  7  31  9.47 31
  8  31  9.19 31
  9  31  9.54 31
  ;
 
PROC GLM DATA=CRACK;
  CLASS AGEF;
  MODEL LOAD = AGE AGEF / P;
  OUTPUT OUT=CRACKREG P=PRED R=RESID;
RUN;
 
PROC PLOT DATA=CRACKREG;
  PLOT LOAD*AGE="*" PRED*AGE="+"/ OVERLAY;
RUN;

```

- ***Reading table from file and data manipulation:***
```
DATA ONE;  
  INFILE 'BIGFILE';
  INPUT GENDER $ ITEM1-ITEM5 X Y Z;
  IF GENDER = 'M' THEN COMPUTE = 2 * X + Y;
  IF GENDER = 'F' THEN COMPUTE = 2 * X;
RUN;

PROC FREQ DATA=ONE;
  TABLES ITEM1-ITEM5;
RUN;

PROC PLOT DATA=ONE;
  PLOT Z * COMPUTE;
RUN;

```

- ***Creating SQL table and plotting:***
```
PROC SQL;
CREATE TABLE CARS1 AS
SELECT MAKE, MODEL, TYPE, INVOICE, HORSEPOWER, LENGTH, WEIGHT
   FROM 
   SASHELP.CARS
   WHERE MAKE IN ('AUDI','BMW')
;
RUN;

PROC SGPLOT DATA = WORK.CARS1;
VBAR LENGTH ;
TITLE 'LENGTHS OF CARS';
RUN;
QUIT;

```

- ***Creating table and Data manipulation:***
```
DATA READIN;
	INPUT Y1-Y6;
  CARDS;
  11 55 59 35 25 87
  12 79 73 74 86 29
  13 80 95 77 25 74
  ;
RUN;
DATA OUT;
  SET READIN;
  ARRAY VALUES Y1-Y6;
  LARGEST = MAX(OF VALUES[*]);
  INDEX    = WHICHN(LARGEST, OF VALUES[*]);
  NAME = VNAME(VALUES[INDEX]);
PROC PRINT;
RUN;

```

- ***Data manipulation, merging and plotting:***
```
data CNS2new;
  set mylib.CNS2;
  if AGE le 60 then AGE60 = 1;
  else AGE60 = 0;
  SEX_AGE60 = SEX*AGE60;
  GROUP_AGE60 = GROUP*AGE60;
  LESSING_AGE60 = LESSING*AGE60;
run;
data temp;
  set CNS2new;
  dummy = 0;
run;
proc phreg data=temp noprint;
  model B3TODEATH*STATUS(0) = GROUP SEX AGE60 SEX_AGE60 dummy;
  output out=temp1 resmart=rr/order=data;
run;
data temp2;
  merge temp temp1;
run;
proc gplot;
  plot rr*KPS_PRE_;
  symbol i=sm60s v=j font=special;
  label rr='Martingale Resid' KPS_PRE_ = 'KPS_PRE_';
run;

```
