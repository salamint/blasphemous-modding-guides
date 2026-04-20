Mod development
===================================

Developing new mods for Blasphemous and Blasphemous II differs a little, but the
principle is the same and the tools are very similar.

.. danger::
   Some tools talked about here allows you to read parts of the (transformed)
   source code of some games and programs.
   The source code of most games are protected with a license or copyrights.
   That does not mean you are not allowed to use these tools and explore the
   code by yourself, but do not under any circumstance share the original source
   code of a program/game for which you don't own the rights to do so.

What is modding?
----------------

In simple terms, modding is writing code that will be injected into the
executable of a program to alter the way it work. It's mainly used for video
games to add new content or change the rules of the game.

How does that work?
-------------------

The executable of the game contains all of the instructions to run the game.
Using tools like `BepInEx`_ or `Melon Loader`_, it is possible to insert your
own instructions in the middle of the game's isntructions.

.. _BepInEx: https://github.com/BepInEx/BepInEx
.. _Melon Loader: https://github.com/LavaGang/MelonLoader

In particular, what we look for is to **patch functions**.
Functions are common block of instructions executed together, that may produce a
result. They are created by the developers of the game to not have redundant
code.

Image a function ``MovePlayerLeft(int pixels)``. It is called ``MovePlayerLeft`` and
takes an integer ``pixels`` in input. It is self explanatory, it will move the
player to the left by the amount of pixels you have indicated it.
Now imagine that this functions is called everytime you press the left arrow key
in game, and you want the player to receive money everytime they move left.
What you want to do is to **patch** this function.

Patching allows you to chose whether the code you want to insert will be
executed *before*, *after* or *replace* the code of the function you have
selected.
In this example it doesn't matter if the money is given before or after the
player moves left, but we do want to keep the player moving left so we won't
whose to replace the function with our patch.

All there is left to do is to write the code that will give the player money (we
can even chose the amount depending on the amount of pixels the player will
move), and give the indications of which function we want to patch and how we
want to patch it.

That is basically all modding is on the *writing* part.

.. _Blasphemous Randomizer Wiki: https://brandenek.github.io/Blasphemous.Randomizer.Wiki/

Great but how to I know which function to patch?
------------------------------------------------

That's a good question. That's the question we're trying to answer when modding,
because depending on the tools that help you take a look at the internals of the
game, the way the game is compiled and distributed, and other factors, it is
difficult to answer.

First, let's explain how Unity games work.

