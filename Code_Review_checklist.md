# CODE REVIEW CHECKLIST
*The main purpose of code reviews is to improve your codebase, improve your team's development skills, share knowledge, 
communicate, and — finally — write good code.*

* Be careful about code format. The team needs to agree on a format and everyone in the team should use that format.

* Ensure that proper naming conventions have been followed. <br/>Follow Java naming convention, f.e.. class names should start with capital letters, method names start with lowercase letters, etc.

* Remove comments if they give no information! Comments should explain why the code is written. Comments may also be used if there are complicated business rules or workaround solutions. Other comments should be removed.

* Attention should be paid to the architectural approach of the written code. The code should split into multiple layers. The MVC design pattern must be maintained and any parts that do not fit the layered architecture should be corrected.

* if there is a hard-coded variable in the code, it must be assigned to a constant or a configuration variable.

* Check that similar variables can be grouped under an enum.

* Verify that existing libraries/classes are used instead of writing code from scratch.
Anything should be removed if another library is used that does the same work as the existing libraries in the application.

*  The purpose of the written code should be understood from the related issue or the code itself. If no code belonging to the requested business rule has been written, it must be corrected.

* The code blocks should be concise. Make sure that the code is separated into blocks and each block has its own and only one responsibility. (Single Responsibility Principle)

* It's better to check whether SOLID principles are applied or not.***

* Code duplication should be checked, if there is a code written for the same purpose in the project, that code should be used or changed so that it can be used. (Don't Repeat Yourself)

* Edit any unreadable and not properly named code. The method or class name should describe its work correctly.

* Be sure that exceptions and errors are handled and logged properly. If the method returns an error code, check that if it describes the error properly.

* The code should be checked for security as possible as you can. Be aware of SQL Injection, XSS, Man in the middle, etc. Specifically, check the implementation behind the HTTP 3xx redirects.

* Performance controls should be done. Possible null pointer exceptions, cache errors, possible lazy initialization exceptions, String + String usages instead of StringBuilder should be fixed.

* checkstyle/ findbugs issues are resolved

# Code review checklist by categories
## Implementation
- [ ] Does this code change do what it is supposed to do?
- [ ] Can this solution be simplified?
- [ ] Does this change add unwanted compile-time or run-time dependencies?
- [ ] Was a framework, API, library, service used that should not be used?
- [ ] Was a framework, API, library, service not used that could improve the solution?
- [ ] Is the code at the right abstraction level?
- [ ] Is the code modular enough?
- [ ] Would you have solved the problem in a different way that is substantially better in terms of the code’s maintainability, readability, performance, security?
- [ ] Does similar functionality already exist in the codebase? If so, why isn’t this functionality reused?
- [ ] Are there any best practices, design patterns or language-specific patterns that could substantially improve this code?
- [ ] Does this code follow Object-Oriented Analysis and Design Principles, like SOLID(Single Responsibility Principle, Open-close principle, Liskov Substitution Principle, Interface Segregation, Dependency Injection)?

## Logic Errors and Bugs
- [ ] Can you think of any use case in which the code does not behave as intended?
- [ ] Can you think of any inputs or external events that could break the code?

## Error Handling and Logging
- [ ] Is error handling done in the correct way?
- [ ] Should any logging or debugging information be added or removed?
- [ ] Are error messages user-friendly?
- [ ] Are there enough log events and are they written in a way that allows for easy debugging?

## Usability and Accessibility
- [ ] Is the proposed solution well designed from a usability perspective?
- [ ] Is the API well documented?
- [ ] Is the proposed solution (UI) accessible?
- [ ] Is the API/UI intuitive to use?

## Testing and Testability
- [ ] Is the code testable?
- [ ] Does it have enough automated tests (unit/integration/system tests)?
- [ ] Do the existing tests reasonably cover the code change?
- [ ] Are there some test cases, input or edge cases that should be tested in addition?

## Dependencies
- [ ] Does this change require updates outside of the code, like updating the documentation, configuration, readme files? If so, was this done?
- [ ] Might this change have any ramifications for other parts of the system, backward compatibility?

## Security and Data Privacy
- [ ] Does this code open the software for security vulnerabilities?
- [ ] Are authorization and authentication handled in the right way?
- [ ] Is sensitive data like user data, credit card information securely handled and stored?
- [ ] Is the right encryption used?
- [ ] Does this code change reveal some secret information (like keys, usernames, etc.)?
- [ ] If code deals with user input, does it address security vulnerabilities such as cross-site scripting, SQL injection, does it do input sanitization and validation?
- [ ] Is data retrieved from external APIs or libraries checked accordingly?

## Performance
- [ ] Do you think this code change will impact system performance in a negative way?
- [ ] Do you see any potential to improve the performance of the code?

## Readability
- [ ] Was the code easy to understand?
- [ ] Which parts were confusing to you and why?
- [ ] Can the readability of the code be improved by smaller methods?
- [ ] Can the readability of the code be improved by different function/method or variable names?
- [ ] Is the code located in the right file/folder/package?
- [ ] Do you think certain methods should be restructured to have a more intuitive control flow?
- [ ] Is the data flow understandable?
- [ ] Are there redundant comments?
- [ ] Could some comments convey the message better?
- [ ] Would more comments make the code more understandable?
- [ ] Could some comments be removed by making the code itself more readable?
- [ ] Is there any commented out code?

## Experts Opinion
- [ ] Do you think a specific expert, like a security expert or a usability expert, should look over the code before it can be committed?
- [ ] Will this code change impact different teams? Should they have a say on the change as well?

# What about coding styles and conventions?
*Cristal-clear coding styles can speed-up your code reviews. But, only if you automatically enforce them via tooling.*

_Crystal-clear coding style_ guides are the only way to enforce consistency in a codebase. 
And, consistency makes code reviews faster, allows people to change projects easily and keeps your codebase readable and maintainable.
