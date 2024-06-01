# ob-skynet.el
emacs org-babel support for skynet.

# Setup
Load The ob-skynet.el to your emacs.
```emacs-lisp
(load ob-skynet.el)
```
set where skynet home is
```emacs-lisp
(setq org-babel-skynet-home <path-to-skynet-home>)
```
and sure skynet is add to PATH.

# How to use

write a start service:

#+BEGIN_SRC skynet 
...
#+END_SRC 

press C-c C-c, the code will be run.
the process will blocked util service end. 
So you need to exit process in code. Otherwise,
you must kill skynet process for backing to emacs.

you can define the name of service, just put the name after the `+++`
#+BEGIN_SRC skynet 
+++main
...
#+END_SRC 

Mutil service is supported.
#+BEGIN_SRC skynet 
+++main
...
+++ping
...
+++pong
...
#+END_SRC 

You can add configuation by Header arg :configs.
For example, specifying the node of code.
#+BEGIN_SRC skynet  :configs "node=\"node1\""
...
#+END_SRC
Notice, the " should be escaped



