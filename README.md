Malicious
=========

ASM Malicious Code - Let's play a game

Create the most undetectable ASM virus that we can using http://www.virustotal.com (55 AntiVirus)

Capacities
* Reproduction by infecting near PE files
* Basic polymorphism
* Communication via 'HTTP'

We start by testing on a HelloWorld sample using g++.
Why ? Because an empty main with gcc will result into 5 flags. HelloWorld with gcc 2 flags. 
And only 1 with g++. Yeah... amazing start. Good job AVs !

<br>
**Version #1**

* creating new section
* changing entry point (EP)
* infect \*.exe in current directory
* get back to old EP

`> 13 flags (out of 54!)`


<br>
**Version #2**

* polymorphism (xoring by random value)

We still expect a lot of flags since it doesn't change our behaviour (in a sandbox)

`> 6 flags. Nice.`

That means half of the flags from version #1 was pattern recognition.
> Strangely, all the flags are from unknown AVs (from the general public). Avast, Avira, AVG are all bypassed.

<br>
**Let's do some testing**

* We note that we only get 1 flag if we don't change the EP in our infected file
* When we create a new section, empty with an exit, only changing the EP to our section
will get us 3 flags
* If we add our virus, without going back to the old EP, we get 13 flags !
* We get the same flags if the virus is not infecting files, just the code is present. Interesting.
* We get different result by using the same infected file : the encryption is sometimes broken

What does this mean
* Most of the AVs do not check the section if it is not executed.
* The action to change the EP to the last section will alert half of the one I have in version #2.
* Even if we do not infect files, a code showing characteristics of doing it will be flagged.

What we can do
* Find an other way to execute our section
* A better encryption
* Blur the way of infecting files

<br>
**Few days later**
Our virus is now flagged by 12 AVs. We've got 6 more who joined the fight. Strangely, 
they all have the same result flag : "Gen:Variant.Graftor.158431". They share informations. 
It makes sense. Variant Graftor must be some kind of pattern recognition for 
virus that infect others and cannot check our virus with single-file signature detection.

<br>
**Version #3**

<br>
**Going deeper**

We know have a good version of the virus. It is mostly undetectable, can reproduce and communicate.
But that's only the beginning. When an AV will detect it (and it will), with our sort of 'polymorphism' we will not be able to hold against a detection based on our signature. Our decrypter can be easi
ly marked, same as our behavior. We could improves our encryption, add junk code or even sandboxes 
detection. But it's just not interesting anymore.
