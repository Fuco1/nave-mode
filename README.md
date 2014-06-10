(note: I don't know when this will get implemented, if ever.  However, you are free to engage in a discussion in the issue tracker :)

# not-a-vim-emulation-mode

(short version: nave-mode, read it as if 'navy' was spelled with 'e' at the end :D)

Vim has this amazing notion of composeable commands: you define motions, then a couple operators and that can pretty much cover any editing operation imaginable.  It is infinitely extensible and very intuitive, if `w` means "move forward a word", `dw` means "delete a word", `yw` means "copy a word" (I think), `cw` means "change a word" and so on: the catch: each of `d`, `y`, `c` etc. are defined in a way to take "any motion"---this means you can define basically any region and `d` will happily work with it.

So, you might say, `evil` already has this!  That's true, but `evil` also aims to be a vim emulation mode.  This is not a vim emulation mode.  It is my attempt to bring into emacs what I find brilliant about vim, while not dragging *all the nonsense* vim uses along---most notably, modal editing (it really is not useful people!).

So while `evil` devs are constraint about their implementation by the behaviour of `vim`, I'm not.  And when I was briefly playing with `evil`, I've already found tons of limitations that are nonsensical: text objects can't be arguments of motions (WHY ON EARTH!), operations are not stackable (for the most part), text-objects are limited to continuous blocks/regions... I don't remember all but I was frustrated.

I was also trying to make [smartparens](https://github.com/Fuco1/smartparens) work with evil in some intuitive way and it was quite impossible.

# What are the aims then?

I want to have

* Stackable operations, or at least a notion of "main" operation and optional filters---like numeric arguments but "basically anything".  One example is the `a` and `i` thing vim has for "around/a" and "inner" text object... that should just be a command filter/pipe/whatever.
* "Text objects" are not just regions---it should be possible to add non-trivial properties to them.  A "balanced pair" might be a text object, trying to kill it would behave in a paredit-like fashion.
* Motions are still motions, implicitly defining "text objects", but since they are a bit crippled by their nature, not everything will work.

What for example is impossible in vim (or at least evil) is to define "move point to inner end of text object"...  Because it is text-object, I can only delete, paste, copy, change... but not move around it.

Because the objects has to contain point, I can't have a "next balanced pair" object, into which I could jump, or which I could jump over.

As many of my packages deal with moving around, this would provide a nice and consistent interface to those as well.

# Disclaimer

I'm not a master vim user and my knowledge of `evil` is superficial at best.  Maybe things here are complete lies, maybe not.  I still want a system that is not vim but has the brilliant stuffs from vim :)
