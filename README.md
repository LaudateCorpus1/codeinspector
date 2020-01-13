# Lint

Lint is a paclet for finding problems in Wolfram Language code.

[Finding Bugs in the Wolfram Language from WTC 2019](https://www.wolfram.com/broadcast/video.php?c=467&p=5&v=2911)


## Installing

Install Lint and dependencies from the public paclet server:
```
In[1]:= PacletUpdate["AST", "Site" -> "http://pacletserver.wolfram.com", "UpdateSites" -> True]
			PacletUpdate["Lint", "Site" -> "http://pacletserver.wolfram.com", "UpdateSites" -> True]

Out[1]= Paclet[AST,0.2,<>]
Out[2]= Paclet[Lint,0.2,<>]
```


## Setup

Lint depends on the AST paclet. Make sure that the paclets can be found on your system:
```
In[1]:= Needs["AST`"]
			Needs["Lint`"]
```

[AST on stash.wolfram.com](https://stash.wolfram.com/projects/COD/repos/ast/browse)


## Building

Lint uses a Wolfram Language kernel to build a `.paclet` file.

Lint uses CMake to generate build scripts.

Here is an example transcript using the default make generator to build Lint:
```
cd lint
mkdir build
cd build
cmake ..
cmake --build . --target paclet
```

The result is a directory named `paclet` that contains the WL package source code and a built Lint `.paclet` file for installing.

You may see an error because the default path to `WolframKernel` may not be correct.

Here is the cmake command using supplied values for `WOLFRAMKERNEL`:
```
cmake -DWOLFRAMKERNEL=/path/to/WolframKernel ..
```

Here are typical values for the variables:
* `WOLFRAMKERNEL` `/Applications/Mathematica.app/Contents/MacOS/WolframKernel`

Here is the build directory layout after building Lint:

```
paclet/
  Lint/
    Kernel/
      Lint.wl
    PacletInfo.m
    ...
```

### Windows

It is recommended to specify `wolfram.exe` instead of `WolframKernel.exe`.

`WolframKernel.exe` opens a new window while it is running. But `wolfram.exe` runs inside the window that started it.


## The Severity levels

### Remark

Issues such as character encoding assumptions, formatting issues.

A character was saved as extended ASCII, and cannot be treated as UTF8.

Token is not on same line as operand.


### Warning

Most likely unintended uses of functions.


### Error

Recoverable errors in syntax.

Code that is never intentional.

`"\[Alpa]"`

`f[a,]`


### Fatal

Unrecoverable errors in syntax.

`1 + {}}`



