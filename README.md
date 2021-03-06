# Challenge
Print 'Hello World' in Node.JS
Without using only a limited set of characters
Allowed Characters:
	!
	+
	[]
	()

## FAQ
* Q: Why?
- A: Why not?

* Q: No, seriously, why?
- A: Well, it's a proof of concept. I think there are now tools online that can convert any piece of JavaScript code into this, there's a fancy name for it too but I can't remember it.
- A: I was inspired by the awesome presentation Wat on https://www.destroyallsoftware.com/talks/wat. The one thing that really struck me is that `true+true+true = 3`. That's where it all started from :)

## Theory
	We can already represent all of the numbers.
	Booleans are easy. ![] = false, !![] = true
	Convert anything to a number: +![] = 0, +!![] = 1
	Convert anything to a string: +![]+[] = '0'
	Addition! +!![]+!![] = 2
	We have a limited set of characters available.
	![]+[] = 'false'
	We can access individual characters (string manipulation)
	[![]+[]][-[]][-[]] = 'f' (index 0 of 'false')
	[![]+[]][-[]][-[]+!![]] = 'a' (index 1 of 'false')
	And so on!

	Handy extras...
	[][[]] = undefined
	[][[]]-[] = NaN

	So we have all of these strings available.
	'false', 'true', 'undefined', 'NaN'

	Therefore all of these characters.
	'a', 'd', 'e', 'f', 'i', 'l', 'n', 'r', 's', 't', 'u', 'N'

	We can write
	'return', 'fill', 'entries'

	...not that much.
	
	BOOYAA! Array.prototype.fill exists. (so does 'entries' but 'fill' is shorter)
	We can do:
	(simplified for sanity's sake)
	[]["fill"] = "[Function: fill]"
	and

	So now we have new characters!
	'a', 'c', 'd', 'e', 'f', 'i', 'l', 'n', 'o', 'r', 's', 't', 'u', 'F', 'N', ':'

	The magic word here is 'constructor'.
	We can do []['constructor']['constructor'](<code>)() to evaluate our own code.
	(Later just as Function(<code>)())

	We can also do some constructor magic.
	(+[])['constructor'] = "[Function: Number]"
	Gives new characters 'b', 'm'

	Which allows us to perform the next step.
	([]+[])['constructor']['name'] = "String"
	
	we can construct
	"toString"

	And call (<number>)["toString"](36)
	which converts any given number to Base 36
	Voila! All of the lowercase characters.

	We can now start assigning some functions to make our program shorter to write.
	
	Function("[]['constructor']['prototype'][0]=[]['constructor']['prototype']")();
	We get the characters "'" and "=" from "".link()
	[]{}() can be get from any given function ("function fill() { [native code] }")

	This is a mouthful, but once done, we can declare:
	Function("[][0][<key>]=function(stuff){return stuff}")();
	and later just call [][<key>]("stuff");

	So simple, ain't it? :)
	Function("[][0][1]=function(f){return f['toString'](36)}")();
