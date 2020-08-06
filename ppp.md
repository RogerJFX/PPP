Programmers' Politeness Policy (3P)
-

Version 0.0.1

---

1. Preface
1. Definition of politeness
1. Definition of good but impolite source code
1. Polite source code
1. Educational aspects of polite code
1. Dependencies
1. Illustration
1. The code review problem
1. Conclusion

---

#### 1. Preface

We all faced many paradigms concerning software development like design patterns, proper documentation, Scrum asf.. 
Any of them should help to improve code quality. Nevertheless, we all know the situation when taking over a software 
project, that might be compliant with all those paradigms, but still we are in trouble for some reason, because we 
can't get the clue in time.

We unavoidably think of ourselves as bad programmers then. But most often we still realize a stale taste once we 
managed to get the point. And often we permanently have to struggle through the project's code later. We all remember
 ourselves swearing at some lines of code, even if we did not know the exact reason.
 
But why? Is it possible the former author simply was impolite, though he did all right and met any so far known compliance?

This is what we discuss here: what is politeness in software development?

---

#### 2. Definition of politeness

There is one main rule of politeness: **don't disturb your neighbor**. 

Consider some people sitting at a table for dinner. Any person is looking forward enjoying his meal. There are requirements like:

- the person should be able to interact with the meal's flavours
- the person will like to have good conversation
- a discreet background will enhance the person's experience 
- the person will appreciate any other person at the table to help him enjoy




---

#### 3. Definition of good but impolite source code

Ok, nearly everybody of us knows Sonarcube. Or design patterns. Or...

It is beyond our scope to discuss all rules of modern high quality software development.

There is one reason to keep this chapter: let us figure out what makes even brilliant code impolite.

**Example a: Lambdas**

Lambdas help us write readable code only if we do not exaggerate. If we do, we often won't understand even our own code 
a couple of weeks later.

**Example b: Macros**

Macros are a very powerful option in languages like C or Scala (there called implicits). They help us build very 
sophisticated code. Exaggeration however will lead to weird constructs, that nobody can see through at once. It really is 
annoying stepping through the code in a common editor without successfully figuring out what happens.

**Example c: The annotation massacre**

Oh yes, this is a common Java problem. There are plenty of frameworks giving us heaven on earth. Saying: we do that for 
you, don't mention, just annotate. Saying: asshole, you are too stupid anyway, so use our annotations. Problem here is, 
that it might work out of the box in a first step, but in a second or third, when it becomes a bit more complicated, 
it most often becomes cruel. Another problem is, that I don't like being called asshole.

**Example d: Bitwise programming**

Bitwise hacking of course is cool and fruitful. And it should lead to an outstanding performance. There are exceptions: if 
a programmer just want's to show his brilliance by writing bitwise code even if it could be done easier and readable, he fails.

**Difference**

In any of the above examples, the techniques are beautiful and therefore good. Only exaggeration makes them awful and thus  impolite.

Difference is just the proportion of the programmer's self profiling. Why doesn't he simply communicate with the readers 
of his code instead? Huu, as friends at last, not as competitor, polite then? Wouldn't it be great?

---

#### 4. Polite source code

Think of a screen giving you a hand while you investigate some foreign code (remembering Salvador Dalí might help).

First of all polite source code must fit all requirements of high quality code. Code smells are forbidden, and crappy 
code of course as well. So code politeness just has to go on top of all other quality standards.

- Code should be self explaining
- It should be easy to read
- Code should rely on compiler or interpreter optimizations
- Code should demonstrate what was in the authors mind (even if it smells, traceability of mind might outstrip anything 
else in some cases)
- Should be easy to debug in as many editors as possible
- Comments are useful, if not too big and thus disturbing the flow of reading the code*.
- Comments should be written in the very same language as the technology itself, so English in most cases.

Just think of those who take over your code later and give em a virtual hand.

\* Should be differed. An Api of course should be extremely documented.

---

#### 5. Educational aspects of polite code

Politeness might even help newbies getting the point. Anybody joins an existing team is a newbie, but there still are 
beginners like junior developers, who aren't that experienced as veterans.

Even veterans do not know everything, but they often want to learn new stuff, and they are happy with it most often. So 
writing polite code gives the opportunity to introduce new techniques with the effect of increasing peoples motivation.

Polite code should take them by the hand in order to help orient themselves. This should be kept in mind when writing 
source code. 

This does not mean, polite code only is an educational method, and of course never code should become too trivial. Just as 
mentioned: politeness has to be on top of the highest quality standards. 

---

#### 6. Dependencies

There normally is no reason to treat this issue, since anything is implicit here. E.g. joining a C++ team will implicitly 
force me writing C++ (hey, what a recognition!). If there are any issues beyond C++, lets say JavaScript, I will try 
to keep the scripts in a C++ style, so anybody within the team, who's most probable a C++ programmer, will be able to 
read my results easily.

So there is only one dependency: **the team**.

---

#### 7. Illustration

This is a small piece of code, I wondered about a couple of days ago. It's Javascript here. Element is the HTML Element.

What I accidentally wrote, is this (yes, I now know there is something like a class list):

~~~
Element.prototype.removeClass = function(clazz) {
	const old = this.getAttribute('class');
	const splitted = old.split(' ');
	const filtered = splitted.filter(item => item !== clazz);
	this.setAttribute('class', filtered.join(' '));
}
~~~

I still ask myself if this won't be better:
~~~
Element.prototype.removeClass = function(clazz) {
	this.setAttribute('class', 
		this.getAttribute('class').split(' ').filter(item => item !== clazz).join(' ')
	);
}
~~~

Hm. Hm... It depends? Hm. Ok, I will refactor that soon. For me it is readable enough.

On the other hand I consider the first version better readable than the second, since nearly everything is declared 
by self explaining field names. 

So it depends. If being member of a Java (7) team, I would consider the first version more polite. As a member of a 
Scala team I would prefer the second version.

---

#### 8. The code review problem

I am over 50 years old, my colleague is about 30.

**Scenario 1**

I wanted to have a code review from my colleague. He decided to claim some changes concerning:

~~~
boolean isReal() {
	if (1 == 2) {
		return false;
	} else {
		return true;
	}
}
~~~

He wanted me to get rid of the `else`. So I went over to him and shouted at him "Silly fool, how dare you teach me programming?"

Was I right?

**Scenario 2**

He wanted me to review his code. His code was:

~~~
boolean isReal() {
	if (1 == 2) {
		return false;
	}
	return true;
}
~~~

I wanted him to change the condition `if (1 == 2)`  to `if (1 == 1)`.

He did it. Was he right? Please don't try to answer, whether I was right or not.

**Scenario 3**

So I told you a lie. I am not over 50, but about 30, so in the end as old as my colleague.

Now to come back to the code of scenario 1. There is nothing wrong with that code and there is nothing wrong with 
the reviewers claim as well. Just a matter of favour and conventions.

What we did? We trashed each other until I have wun. He was beaten, he is my slave from this moment on. I instantly gave my mummy a call 
just to make her another bit prouder of me.

This was another lie? Yes, I agree, I am indeed over 50. I simply did what he wanted, just because I found other occurrences
in the project, where others did it his way. Simple like that. Besides, I would not have called my mummy.

---

#### 9. Conclusion

It's as easy as that: write good code and give your mates as many hugs as possible. Stop barking, stop insisting of 
being right, stop being the coolest and best programmer ever even if your mama would be as proud as a peacock.
