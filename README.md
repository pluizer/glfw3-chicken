# CHICKEN GLFW3 Bindings

## Description
Bindings to the [GLFW](http://www.glfw.org/) OpenGL window and event management library, version 3.X.

## Requirements
None

## Documentation
Direct bindings generated by [bind](http://wiki.call-cc.org/eggref/4/bind). Names Schemeified, with GLFW prefices removed. Constants surrounded by `+`s (e.g. `+alpha-bits+`)

Version 3 of GLFW is not backwards compatable with previous major versions of GLFW.

For information regarding the GLFW API, see the official [GLFW documentation](http://www.glfw.org/documentation.html).

## Example
This example must be compiled due to the external function definition.

``` Scheme
(import foreign)
(use (prefix glfw3 glfw:))

(define-external (keyCallback (c-pointer window)
                              (int key) (int scancode) (int action) (int mods))
    void
  (cond
   [(and (eq? key glfw:+key-escape+) (eq? action glfw:+press+))
    (glfw:set-window-should-close *window* 1)]))

(glfw:init)

(define *window* (glfw:create-window 640 480 "Example" #f #f))

(glfw:set-key-callback *window* #$keyCallback)

(let loop ()
  (glfw:swap-buffers *window*)
  (glfw:poll-events)
  (unless (glfw:window-should-close *window*)
    (loop)))

(glfw:destroy-window *window*)
(glfw:terminate)
```

## Author
Alex Charlton

## Licence
Copyright (c) 2014, Alexander Charlton
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
