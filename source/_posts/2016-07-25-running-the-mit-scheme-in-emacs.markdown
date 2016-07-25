---
layout: post
title: "Running the MIT-Scheme in Emacs"
date: 2016-07-25 07:07:18 +0000
comments: true
categories: Emacs
---

Based on the Ubuntu14 OS platform. I choose the x64-version mit-scheme source code.

[GNU'S mit-scheme](http://ftp.gnu.org/gnu/mit-scheme/stable.pkg/9.2/mit-scheme-9.2-x86-64.tar.gz)

```bash
tar xvf mit-scheme-9.2-x86-64.tar.gz
cd mit-scheme-9.2/src/
apt-get install m4
./configure
#Build the software:
make compile-microcode
make install
```

I changed the .emacs config file yet.

```elisp

;;Always do syntax highlighting
(global-font-lock-mode 1)
;;Also highlight parens
(setq show-paren-delay 0
   show-paren-style 'parenthesis)
(show-paren-mode 1)
;;This is the binary name of my scheme implementation
(setq scheme-program-name "mit-scheme")
	   
```

When you setup mit-scheme finish. You should be restart the Emacs to reload your new configuration for this.
And Create a new lisp file, like 'test.scm', using the emacs open it. Using the `C-x 2` to open a other window, running the `M+X run-scheme`.

You get in the MIT-Scheme's REPL environment. Take a try `C-x C-e` to running the scheme code. and it should be return the resulte on the first window.

```scheme
(define (square x)(* x x))
(square 9)
```
