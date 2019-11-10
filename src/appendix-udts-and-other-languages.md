## UDTs and other languages

It is possible to use your UDTs with other languages, but you need to be careful.

In vast majority of cases, you will need to duplicate the UDT definition in given language.

UDT [memory representation](chapter_01-02-00-memory-representation.html) always contains just the elements, and that is what you can pass to 3rd party DLL.

> **Note:** thinBASIC specifics, such as UDT FUNCTIONs or default values cannot be transfered.
