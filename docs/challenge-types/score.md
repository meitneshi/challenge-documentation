## Score challenge

When you are creating a code mission, the user has two ways to execute the code ([see more information on main page](/)):  

* Run -> will only run the code without any test
* Submit -> will run the code with tests you have wrote.


You are able to return a *score* when you test the user code.
For instance if you consider 50 out of 100 tests succeeded you must write it that way (depends of the language):

```java
> Java
Mission.INSTANCE.done(50);

> Python
Mission.done(50)
```

You also have to specify within the `challenge.yaml` different fields:
```yaml
 score:
    min: 0 # default min score, can be omitted
    minToValidate: 90
    max: 100 # default max score, can be omitted
```

At the end on the interface your users will get a new tab next to the **Console**.
![Example score Python](../../img/example-score.png)

### Example
[code_score_python](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_score_python)