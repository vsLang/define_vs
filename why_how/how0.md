# How do I make your own programming language from scratch?

Federico Tomassetti (PhD in Software Engineering) answered in Jul 25, 2017

There are different ways you can build a language.

Let’s assume you want to build a simple textual language (you can also create graphical or tabular languages but let’s put that aside for now).

## Design

Obviously you need first of all to design your language:
```
    what your language will be used for?
    What it will be great at?
    How your approach will differ from others?
    Are you trying to build a general purpose language (like Java or Python) or a Domain Specific Language (i.e., a very specialized language, very good to do one thing)?
    Is your language going to be statically or dynamically typed?
    Who is going to be your ideal user? A Java programmer? A scientist?
    Will your language be similar to some other language in particular?
```
You answer these and many more questions and you get a first idea of your language.

## Grammar

To implement your language the very first thing you need to do is to define the grammar. Typically you want to define an EBNF grammar and then use a tool like ANTLR to generate a parser. This part is relatively easy. Basically you have just to describe what statements will be supported by your language, how expressions will look like, the control flow structures and so on. You can look at these collections of grammars to understand what kind of effort you need to provide.

Basically from the grammar you generate a parser and the parser is a piece of code that is able to process the code written in your new language, recognize the different pieces and give you a representation in memory of the information present in the code. This representation is called Abstract Syntax Tree (AST).

## Validation

Once you have the AST you still need to verify that it is correct because the code could respect your grammar and still be wrong. For example if you use a variable that is not defined or you define twice two classes with the same name, or if you try to sum two incompatible values. You basically need to resolve references, enforce typesystem rules and perform other semantic checks.

## Execution

Ok, you have parse the code, got an AST and verified it is valid. Now you need to do something with it. You can generate code of another language (transpilation). This is for example what most languages for the web do: they generate JavaScript in the end. More traditional techniques consist in writing a compiler or an interpreter. A compiler is something that produces either a native application or some form of executable, like JVM bytecode. An interpreter is instead a program that looks at your AST and execute commands depending on the content of the AST. Typically writing an interpreter is much easier. You can also write both an interpreter and a compiler, or start with an interpreter and later write a compiler. Read here for more discussion on the differences between a compiler and an interpreter.

## Now what?

I described the typical path, now, while this is a map you need more details to execute it, so I have put together a few resources:
```
    A collection of 68 resources on creating programming languages
    A webpage with a free course on building languages
    I have also a book on the subject but I do not link it here to avoid self promotion
```
I hope it helps and have fun creating your own programming language!