# Echoes of Eternity

Echoes of Eternity is a Magic: the Gathering card that does some pretty crazy things. The math required to figure out how it all works is best done by machine instead of frantically at the table (while some number of players may be waiting on you).

This simple HTML page does that.

## Background

This small project started off seeking an answer to the question: If I have a Mirage Mirror, am I better off copying a Glaring Fleshraker, or am I better off copying an Echoes of Eternity? The short answer: Copy the Echoes of Eternity! For the long answer, check out [the math](#the-math).

## The Math

The math is simple. Explaining it to a table full of people who aren't rules nerds or programming nerds is not.

The text of the card is (the card's text carries a copyright from Wizards of the Coast from 2024):

> If a triggered ability of a colorless spell you control or another colorless permanent you control triggers, that ability triggers an additional time.
>
> Whenever you cast a colorless spell, copy it. You may choose new targets for the copy. (A copy of a permanent spell becomes a token.)

If you have two of these in play -- let's call them Card A and Card B -- and then cast a colourless spell, Card A and Card B will each trigger for the spell. Then, Card A will trigger for Card B's trigger, and vice versa; it's a simple squaring.

$$g = e^{2}$$

If you control a Glaring Fleshraker and some number of Echoes of Eternity, you might want to know what happens when you cast a colourless spell.

The text of Glaring Fleshraker is (this card's text carries a copyright from Wizards of the Coast from 2024):

> Whenever you cast a colorless spell, create a 0/1 colorless Eldrazi Spawn creature token with “Sacrifice this token: Add {C}.”
>
> Whenever another colorless creature you control enters, this creature deals 1 damage to each opponent.

Thus, if you cast a colourless spell with one Fleshraker and 1 Echoes of Eternity, a number of things will happen in sequence (with stack contents in parenthesis):

1. Cast a spell (the spell) [Note: This will be copied by Echo of Eternities, but for simplicity sake, it is being skipped for now]
2. A trigger from Glaring Fleshraker to make an Eldrazi Scion token (the spell <- make a token)
3. A trigger from Echoes of Eternity to copy that trigger (the spell <- make a token <- copy trigger)
4. Echoes of Eternity trigger resolves (the spell <- make a token <- make a token)
5. One token is made (the spell <- make a token)
6. A trigger from Glaring Fleshraker to do a damage (the spell <- make a token <- do a damage)
7. A trigger from Echo of Eternity to copy that trigger (the spell <- make a token <- do a damage <- copy trigger)
8. Echoes of Eternity trigger resolves (the spell <- make a token <- do a damage <- do a damage)
9. One damage is done (the spell <- make a token <- do a damage)
10. One damage is done (the spell <- make a token)
11. The original token is created (the spell)
12. A trigger from Glaring Fleshraker to do a damage (the spell <- do a damage)
13. A trigger from Echo of Eternity to copy that trigger (the spell <- do a damage <- copy trigger)
14. Echo of Eternity trigger resolves (the spell <- do a damage <- do a damage)
15. One damage is done (the spell <- do a damage)
16. One damage is done (the spell)
17. The spell is back on the stack

A total of four damage was done and a total of two tokens were made.

Adding more Fleshrakers of Echoes of Eternities to the mix will _rapidly_ get out of hand.

Conventions:

```
f = number of fleshrakers in play
e = number of echoes of eternity in play
t = number of tokens created
g = number of echoes of eternity triggers
d = total damage done
```

$$t = f + f * g$$

Or, in simplified format:


$$t = f(g + 1)$$

In terms of only Fleshrakers and Echoes of Eternity: 

$$t = f(e^{2} + 1)$$

How much damage when all those tokens enter?

$$d = t * (g + f)$$

In terms of only Glaring Fleshrakers and Echoes of Eternities:

$$d = f(e^{2}+1) * (e^{2} + f)$$

Simple, right? Just use the calculator and everything will be easier.
