![Cohesion](../master/clean-code/clean_code_cohesion.png)
![Coupling](../master/clean-code/clean_code_coupling.png)
![Composition](../master/clean-code/clean_code_composition.png)

## Meaningful names
- Intention-Revealing names (Why exists, What it does, and how it is used)
- Use verbs for function names and nouns for classes and attributes.
- A variable should represent the value it was created for. (avoid var x, instead use var customersIndex)

## Naming conventions
- [X]DO choose easily readable identifier names.
- [X] DO favor readability over brevity.
- [X] DO use semantically interesting names rather than language-specific keywords for type names. For example, GetLength is a better name than GetInt.
- [X] DO NOT use abbreviations or contractions as part of identifier names. For example, use GetWindow rather than GetWin.
- [X] AVOID using identifiers that conflict with keywords of widely used programming languages.
- [X] DO NOT use any acronyms that are not widely accepted, and even if they are, only when necessary.

## Small Methods
* A method should be a single testable unit doing only one thing.
* Keep it from 10 to 15 lines of code.
* If your method is bigger, then is probably doing a lot of things that are not their responsibility.
* Prefer ‘Early return’.

## Best practices
* _*Boy scout rule*_. Leave the campground cleaner than you found it. Every time you are writing code, let’s clean the old code a little, it doesn’t matter if is code that someone else writes. Do a small contribution by cleaning around a little. Just don’t go crazy cleaning a lot or you can break something.
* _*Keep It Super Simple*_. Remember, do not overengineer; do not kill a fly with a hammer.
* _*YAGNI (You Ain’t Gonna Need It)*_. Don’t write a factory design pattern thinking that you might need to add more functionality in the future. Wait until that moment and create the factory, but not before.
* _*Principle Of Least Surprise*_. Let’s find a place for each thing, and put it where is more expected to be found by other developers. Put it where it is least likely to cause a surprise when someone finds it.
* _*If it ain’t tested, it’s broken”*_ Write lots of tests, especially unit tests, or you’ll regret it.
* _*Classes and functions should be small and obey the Single Responsibility Principle (SRP)*_
Functions should be no more than 4 lines and classes no more than 100 lines. Yep, you read that correctly. They should also do one and only one thing.
* _*Functions should have no side effects*_
Side effects (e.g., modifying an input argument) are evil. Make sure not to have them in your code. Specify this explicitly in the function contracts where possible (e.g., pass in native types or objects that have no setters).
* _*DRY*_. Avoid duplicate code by abstracting out things that are common and putting these in a single location.
* _*Later equals never*_. You are writing //TODO but you know deep in your heart that you’ll never do that. A good practice is to add a work item in the backlog every time you write a TODO.
* _*4 Code reviews rule*_. In order to be completely sure you are following all standards, best practices, etc, 
you should always request code reviews to 4 persons: 
  * any dev around
  * another dev around 
  * your tech lea 
  * and most important YOU. 

You should always do a code review to your code the same way you will review someone else’s code.
* _*Code Analysis Tools*-. Tools like Resharper, IDE Enterprise Editions, SonarQube, SpotBugs, can help you to adhere to the most common and critical code disciplines.

