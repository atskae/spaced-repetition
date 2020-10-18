# Spaced-Repetition
Learning how [spaced repetition](https://en.wikipedia.org/wiki/Spaced_repetition) works with flashcards and how to implement the algorithm.

## Algorithms
[Leitner System](https://en.wikipedia.org/wiki/Leitner_system)
* Boxes labled 1 through 5. A card moves up a box (for example, from Box 1 to Box 2) when the learner is able to recall the answer.
* A card moves down a box (or resets to Box 1) when the learner cannot remember the term

[SuperMemo](https://en.wikipedia.org/wiki/SuperMemo)
* Many improved versions of this algorithm
    * Named `SM-X`, where `X` is the algorithm version
    * `SM-18` released in 2019
* User rates a card from 1 to 5 (1 being difficult to recall, 5 being the easiest to recall)
    * Cards labeled "more difficult" are reviewed more frequently
* Sudo-code of `SM-2`:
    * `card` object contains the following fields:
        * `rep` repetition number: the number of times in a row that this card was recallable (this value is reset when user is unable to recall the card)
        * `interval` inter-repetition interval: the time (in days) between repetitions
        * `ease` easiness: how easy it is to recall this card
    * `grade`: user-provided grade: between 1 to 5 (where 1 is most difficult, and 5 is most easy)

```
sm2(card, grade):
    if grade >= 3: # user got the correct answer
        if card.rep == 0:
            card.interval = 1 # review this card in 1 day
        elif card.rep == 1:
            card.interval = 6 # review this card in 6 days
        elif card.rep > 1:
            card.interval = card.interval * card.ease
        
        card.rep = card.rep + 1 # increase the recallable streak
        card.ease = card.ease + (0.1 - (5-grade) * (0.08 + (5-grade) * 0.02))
    else: # user was not able to recall this card, or had difficulty doing so
        card.rep = 0 # reset the recallable streak
        card.interval = 1 # review this card in 1 day
        if card.ease < 1.3:
            card.ease = 1.3
```
* The creator (Piotr Wozniak) also developed [incremental learning](https://en.wikipedia.org/wiki/Incremental_reading)
    * Creating flashcards out of text (articles, books). Users simply import text to learn from
    * Retain information from reading
* [Research paper on SM-5](https://www.semanticscholar.org/paper/Optimization-of-repetition-spacing-in-the-practice-Wo%C5%BAniak-Gorzela%C5%84czyk/061ccfaff34c8f9a7eb539524919b08d7d81ef00?p2df)

## Source Code to Study
* [Anki](https://github.com/ankitects/anki)
