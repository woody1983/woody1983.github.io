---
layout: post
title: "GNU Emacs and MIT Scheme on Mac OS X"
date: 2016-08-01 06:37:51 +0000
comments: true
categories: [Lisp, Scheme, Emacs]
---

First, download the MIT/GNU Scheme binary for Mac OS X and copy it to your Applications directory. Then configure Emacs to use the downloaded binary by adding the following lines to your `.emacs`.

![sicp](http://i.imgur.com/1ZGjEDn.jpg)

Via: [Praveen's Blog](http://praveen.kumar.in/2011/03/06/gnu-emacs-and-mit-scheme-on-mac-os-x/)

```scheme

(setq scheme-program-name "/Applications/mit-scheme.app/Contents/Resources/mit-scheme")
(require 'xscheme)

```

```scheme

; Compute the square root of a given number using successive
; approximation.

(define (sqrt value)
  (define (is-good-enough? guess value)
      (< (abs (- (* guess guess) value)) 0.0000001))
	  
  (define (try guess value)
    (if (is-good-enough? guess value)
        guess
        (try (/ (+ guess (/ value guess)) 2) value)))
					
(try 1 value))

(sqrt 4.0)

```

Invoke the Scheme process by `'M-x run-scheme'`. Send the Scheme buffer to the Scheme process by `'M-o'` and now you are able to run Scheme programs from Emacs.
