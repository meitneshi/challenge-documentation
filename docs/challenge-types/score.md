# Score challenge

When you are creating a code mission, the user has two ways to execute the code ([see more information on main page](/challenge-documentation)):  

* Run -> will only run the code without any test
* Submit -> will run the code with tests you have wrote.


You are able to return a *score* when you test the user code.
For instance if you consider 50 out of 100 tests succeeded you must write it that way (depends of the language):

```Java tab=
public static void main(String[] args) {
    // test user code
    Mission.INSTANCE.done(50);
}

```

```Python tab=
def main():
    # test user code
    Mission.done(50):
```

You also have to specify within the `challenge.yaml` different fields:
```yaml
 score:
    min: 0 # default min score, can be omitted
    minToValidate: 90
    max: 100 # default max score, can be omitted
```

At the end on the interface your users will get a new tab next to the **Console**.
<!--
    Pay attention about resources paths :
    mkdocs generates from each markdown file a folder with the same name and its related index file
    So, <path>/my-page.md will create <path>/my-page/index 

    example:
    example-score.png in 'https://deadlock-resources.github.io/challenge-documentation/challenge-types/score/'
    points to the path 'https://deadlock-resources.github.io/challenge-documentation/img/example-score.png'
-->
![Example score Python](../../img/example-score.png)

### Example
[code_score_python](https://github.com/deadlock-resources/challenge-examples/tree/master/example/code_score_python)