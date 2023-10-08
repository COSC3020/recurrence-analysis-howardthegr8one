[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=11908412&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

# My Answer:

$T(n) = 1$ when $n \leq 1$ and $T(n) = 3T(n/3) + 2n^2 + n$ when $n > 1$
My process behind this recurrence relation is that the function recursively calls itself
three times, with $n/3$ as the argument in $T(n)$, it also has two nested loops that iterates
n squared times, thus $2n^2$, and a third loop that iterates $n$ times. From this I 
concluded that $T(n) = 3T(n/3) + 2n^2 + n$ when $n > 1$. Subbing the equation
into itself yields:

$T(n) = 3T(n/3) + 2n^2 + n$

$T(n) = 3(3T([n/3]/3) + 2(n^2)/3 + (n/3) )$

$T(n) = 9T(n/9) + 4n^2 + 2n$

$T(n) = 27T(n/27) + 6n^2 + 3n$

Seeing a pattern I generalized the equation as:

$T(n) = 3^iT(n/3^i) + (2 + i)n^2 + in$

Where $i$ is the number of recursive calls. In this case the number of calls being $log_{3}(n)$
seeing as $n/3$ is the argument given in each call. Thus $i = log_{3}(n)$. Now we can simplify
the equation:

$T(n) = 3^{log_{3}(n)}T(n/[3^{log_{3}(n)}]) + (2 + log_{3}(n))n^2 + n \cdot log_{3}(n)$

$T(n) = n + 2n^2 + n^2 \cdot log_{3}(n) + n \cdot log_{3}(n)$

Or

$T(n) = n(1 + 2n + n \cdot log_{3}(n) + log_{3}(n))$

Ignoring constants and lower terms the theoretical runtime is $O(n^2)$




