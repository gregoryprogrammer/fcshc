fcshc
=====

Controller for fcsh shell.

IDEA
----
Using mxmlc to compile ActionScript is very slow, because each time the whole
code is recompiled. Flex SDK provide tool **fcsh shell** which can speed up this
process by _incremental compilation_. Unfortunately usage of that shell is
inconvinient. Mainly by need to type each time **compile 1** command to
recompile changed part of code (arrow up to doesn't work).

DESCRIPTION
-----------
**fcshc** runs fcsh process for each different mxmlc command in
background. When the mxmlc command (with parameters and source file) is
repeated then **compile 1** command is sended to the right fcsh.


HOW I CAN USE IT?
-----------------
The best way of use it is placing **fcshc** in /usr/bin/ or $PATH and create
appropriate _makefile_ for your project.

Example **makefile** <br/>
<pre>
MXMLC=fcshc mxmlc
OPTIONS=-static-link-runtime-shared-libraries=true
MAIN=Main.as
SWF=output.swf
 
all:
	$(MXMLC) -sp $(OPTIONS) $(MAIN) -o $(SWF)

run:
	flashplayerdebugger $(SWF)
</pre>


NOT WORKING?
------------
If something goes wrong and you will get output like this
<pre>
(fcsh) fcsh: Target 1 not found
</pre>
invoke **fschc stop** and it will stop all fcsh processes and clean up lock 
dirs. Then correct your command (usually parameters) and try again. When I
add output parser (TODO) the manual stopping will not be necessary.


CHANGELOG
---------

#### 0.1
- start


TODO
-----
- check if mxmlc starts compiling (check parameters)
- output parser
- lock output to end of compilation
