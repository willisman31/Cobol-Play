# Teach Yourself COBOL in 24 Hours

## Ch 1

- COBOL is a compiled language
- COBOL is optimized for computing a large number of simple transactions
- COBOL programs are forward-compatible: they should still compile on newer compilers
    - this is the result of the ANSI COBOL standard
- COBOL is a structured language
    - it does still support "GO TO" statements, but these are discouraged

## Ch 2

- COBOL programs have a maximum of 80 characters per line
    - columns 1-6 are reserved for line numbers
        - these are not mandatory
    - column 7 is an indicator space-
        - an asterisk (\*) indicates a comment
        - a dash (-) indicates a continuation of the above line
        - a slash (/) indicates a new page
            - for printing of a program
        - a D in column 7 indicates debugging mode and the line is only included when the program is compiled in debugging mode
        - any other character in col 7 is ignored by the compiler
    - *Area A* = columns 8-11
        - 
