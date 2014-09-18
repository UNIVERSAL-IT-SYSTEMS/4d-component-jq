4d-component-jq
===============

A 4D v14 implementation of the [jq](http://stedolan.github.io/jq/) program.

Calls the program appropriate for platform via LAUNCH EXTERNAL PROCESS.

Command-line argument escape (single quote on Mac, double quote on Win) is intrinsic.

Note that the binary is located in the database folder. This is because in C/S the executable bit is lost if placed inside the Resources folder. As such, the shared component method is marked as "Execute on Server".

Example
-------
```
C_TEXT($url;$jsonString)
C_OBJECT($json)

$url:="https://api.github.com/repos/stedolan/jq/commits?per_page=5"

$status:=HTTP Get($url;$jsonString)

$json:=JSON Parse(JQ_Execute ($jsonString;".[0]"))

$json:=JSON Parse(JQ_Execute ($jsonString;".[0] | {message: .commit.message, name: .commit.committer.name}"))
```

Platform
--------
Windows binaries (32/64 bits) are 1.4 pre-compiled version 1.4 downloaded from [jq](http://stedolan.github.io/jq/).

OS X universal-binary (32/64 bits) was compiled from source.
