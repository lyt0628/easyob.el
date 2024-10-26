# ob-easyob.el
easyob is util macro for user to define ob execution. 

# Features
- Easy to use. with simple macro and keyword, you can  support babel for any program.
- Template varialbes0 Support. Some pre-defined varialbes can be used, which make definition flexiable.
- Async support. you can define a async babel execution for some long time task.

# get started

## Setup
clone repository and Load The ob-skynet.el to your emacs.
```emacs-lisp
(load easy-ob.el)
```

## Simple Example
```emacs-lisp
 (easyob-def tex
 "pdflatex -shell-escape -output-directory=$FILE_DIR  $FILE  && pdftoppm $FILE_SIMPLE.pdf -png $FILE_SIMPLE"
 :extension ".tex"
 :file "$FILE_SIMPLE-1.png")
```

easyob-def is only API easyob provied.
the declaretion of easyob-def is
```emacs-lisp
(easyob-def NAME COMMAND &rest OPTIONS)
```
- name is id for your babel execution. default, you will use the name as language in your org code block
- command is the shell command to execute your binary. with some pre-defined variables, it is easy to custom you command. see  [Pre-defined Variables](#pre-defined-variables) for more information.
- options is optional plist style args for more detail definition. see [Avaliable Keywords](#avaliable-keywords) for more information.


## Pre-defined Variables
- $FILE 
    the full name of temp file.
- $FILE_DIR
    the directory name of temp file. Assuming the temp file is /temp/aaa.c, $FILE_DIR reference to /temp
- $FILE_BASE
    the base name of temp file, in /temp/aaa.c example, $FILE_BASE is aaa
- $FILE_SIMPLE
    the simple name of temp file, as above, $FILE_SIME reference to /temp/aaa. that is $FILE_DIR/$FILE_BASE
- $BODY 
    the variables reference to the final content of code block

## Avaliable Keywords
- :extension <extension>
    the file extension  of temp file and src code of program.
- :file <filename>
    the file of final output, if your program generate a file as results, it is where you indicate your generated file.
    this keyowrd support pre-defined varialbes.
- :async [t|nil]
    if t, run command in async mode, default is nil.
    if you use async mode, the final value cannot be catch by emacs,and you cannot get information from your code(TODO: change it)
- :complete-check-regx <regular expression>, :complete-prefix <prefix> and :complete-subfix <subfix>
    easyob will use regular expression that keyword :complete-check-regx provied to check original content of code block. 
    if pass, do nothing. set content of code block to `<prefix> <original content> <subfix>`
- :head <head-str>, :tail <tail-str>
    the head-str will be add to the beginning of content and the tail-str will be add to the end of content.
    the final content of code block is `<head-str> <prefix> <original content> <subfix> <tail-str>`
- :filename-prefix
    the prefix of temp file and src code of progam
- :lang <language>
    you will use <language> in code block. default <language> is the symbol name of Param name
    ```org
    #+BEGIN_SRC <language>
    ...
    #_END_SRC
    ```
