
### Sandbox
There is also an other mission mode, sandbox one. Common mission must contains a list of test
to allow the user to succeed the mission. But sometimes it can be painful or impossible to implement test to make sure the
user understood and succeed well the challenge. So you can also create a mission without any test but you still have to create
the Run class. The professor will be able to validate the mission via the student page.  
The only thing to add is `sandboxed: true` to the challenge.yaml file.
Example:  
```yaml
name: code_interview_card_game
label: Card Game
description: Card Game
level: ewok
type: CODING
sandboxed: true
```


### Blacklist words
By default there are some words the user cannot use into his code. You can find example into `resources/default/blacklist`.
You can also create your own blacklist for your mission by creating a blacklist file next to the challenge.yaml, then fill it as a csv file. It also supports regex expressions.
Example of blacklist file:  
```bash
[^<>](<|>)[^><],(System\.exit\()(\d)*(\)),(Runtime\.getRuntime\(\)\.exit\(\d*\))
```
