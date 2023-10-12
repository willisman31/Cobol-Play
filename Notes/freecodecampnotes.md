# FreeCodeCamp Course Notes [Course Link](https://www.youtube.com/watch?v=RdMAEdGvtLA)

- COBOL = Common Business-Oriented Language; designed for business functions: performing lots of data-driven transactions continuously
- COBOL is designed to align closely with the English language
- COBOL is standardized and has gone through several revisions; nearly all revisions are forward-compatible, meaning that code from previous versions of the standard should still be compilable and runable by newer compilers and engines
- COBOL is "column-dependent"
    - COBOL expects certain declarations/variables/etc. to be at certain column positions on a given line
    - this quirk is due to COBOL's punch-card driven past

## COBOL Columns

* 1-6 : Sequence Number Area -> space for labels for each line
    - initially were used to make sure that punch cards were fed in order, but have little utility now (if you feel desperate to find a use, some people will mark lines as "TEST" or "DEBUG" in this section) 
    - they do not impact compilation or execution
    - sequence numbers do not need to be unique
* 7 : Indicator area -> marks line as comment, continuation, debug, or form-feed
    - comment: "*" in this space marks the rest of the line as a comment
    - continuation: "-" means this line continues the command from the previous line
    - debug: "D" means this line will only be compiled when the program is in debug mode
        - debug mode may be specified in the SOURCE_COMPUTER paragraph as WITH DEBUGGING MODE
        - if a program is compiled regularly (i.e. not in debug mode), then the "D" will be treated as a "*"
        - in debug mode, values of identifiers are printed via stdout
* 8-11 : *A* Area -> used for elements that give COBOL programs their structure; these include the following:
    - division header
        - COBOL is broken up into the following types of "divisions":
            - identification
            - environment
            - data
            - procedure
        - they appear in the above order in a program
    - section header
        - sections are user-defined parts of a program, each with their own name
        - sections are logically contained within divisions
    - paragraph header/name
        - indicates the beginning of a user-defined section of a program contained logically by a section
    - level indicators/numbers
        - used for specifying data types 
    - DECLARATIVEs and END DECLARATIVEs
        - used for special conditions within code
        - basically, a section of code to USE when an event occurs (different from if statement)
    - END PROGRAM header
        - indicates end of COBOL program; mandatory except in an outermost program with no nested or trailing programs
* 12-72 : *B* Area -> where all the logic hangs out; the part of the program that actually does stuff
* 73-80 : Identification Area -> to be used at programmer's discretion; ignored by the compiler; also called "comment area"

## Program Structure

- COBOL uses a hierarchical structure for program formatting; this is shown below:

```
## DIVISION

### SECTION

#### PARAGRAPH

##### SENTENCE

###### STATEMENT
```

- statements are singular directives; single command words
- multiple statements will go into a sentence which is terminated by a "period separator" (just a period)
    - an "END-<statement>" may also be used instead of a period and will do the same thing, but may make a program easier to digest visually
- statements go into paragraphs, which are kind of like functions in modern languages
- paragraphs go into sections; sections may be user-defined or may be predefined by COBOL
- sections go into one of four divisions:
    1. IDENTIFICATION: metadata about the program- name, author, date, version, etc.
    2. ENVIRONMENT: link between program and the system on which it's running; 2 sections:
        1. set computer environment
        2. map between files in program and files in datasets
    3. DATA: sets up data variables for programming running and what will be lost when the program terminates
    4. PROCEDURE: where all the paragraphs/sentences go; program functionality lives here

## Variables

- variable = map of a name to a data value
- data name = COBOL version of a variable
- variable names must be 30 chars or less, be made up of numbers, letters, or hyphens
    - may not be a reserved word
    - may not contain spaces
- statically typed
    - types may be numeric, alphabetic, or alphanumeric
    - data sizes/lengths must be specified
        - default is 1
    - numeric:
        - PIC 9 -> means single numeric value
            - PIC 9(4) -> means 4-digit numeric value
        - max size len 18
        - decimals:
            - PIC 9(4)V99 -> V represents decimal positions; 99 represent 2 more digits after decimal, 4 digits before
        - money:
            - PIC $9,999V99 -> represents 4-digit monetary value with 2 digits after the decimal
    - alphabetic:
        - PIC A -> single alphabetic character
            - PIC A(8) -> means 8 character value
        - max size length 255
    - alphanumeric:
        - PIC X -> single alphanumeric char
            - PIC X(30) -> 30-character alphanumeric value
        - max size length 255
- literals = unchanging variable values
    - COBOL comes with several pre-set options including the following:
        - ZERO/ZEROES
        - SPACE/SPACES
        - LOW-VALUE
        - HIGH-VALUE
        - NULL/NULLS

## Data Division

- 