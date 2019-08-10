First: Clangd's automatic header inclusion is a seriously amazing feature. you know this, but I have to say it.

*Problem*: When an include path in the flags contains a symlink, header inclusion doesn't work .

*Steps to Repro*

Ensure clangd options include `-background-index`

1. clone this repo
2. edit the run `sed 's#CWD#'$(pwd)'#' compile_commands.json.template > compile_commands.json`
3. open src/test.cc
4. try to insert 'IncludeTest' and have header insertion work

*Expect*:

* Header is inserted as `#include <Include.h>`

*Actual*:

* With clangd 8: full, absolute path is inserted
* With clangd trunk: no inlude is inserted


See: 

[![asciicast](https://asciinema.org/a/BNfFJqUmNacLKWnaAkFUEI0UW.svg)](https://asciinema.org/a/BNfFJqUmNacLKWnaAkFUEI0UW)
