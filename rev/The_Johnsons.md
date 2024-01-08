# The Johnson's
Running `main` shows a program that asks for the favorite colors and foods of 4 people. In order to get the flag, we must supply the correct answers to each question.
![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/946ae9b5-ef79-497b-8a23-9bd35c85ffdd)
I loaded the program into IDA Free and immediately the `main` and `check` functions came to my attention. `main` simply asked for user input and ensured we don't input a particular food or color option more than once. The `check` function was also relatively straightforward.
![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/2fe2f045-ecf4-4051-95ef-f44310fcd526)
To solve this challenge, our inputs have to make each item in the if-statement **false**.

Therefore:
 - `chosenFoods[2]` and `chosenFoods[3]` must not equal `3` (We want `v0` to be true, so that `v1` can be true in order to pass the negation in the if-statement.)
 - `v0` must be true and `chosenColors[1]` must not equal `1` (We want `v1` to be true, to pass the negation in the if-statement.)
 - `chosenColors[0]` and `chosenColors[1]` must not equal `3` (We want `v2 to be true, to pass the negation in the if-statement.)
 - `chosenFoods[0]` must equal `4`
 - `chosenFoods[3]` must not equal `3`
 - `chosenColors[2]` must not equal `4`
 - `chosenColors[3]` must not equal `2`

Following these rules leads us to conclude that:
- `chosenFoods = [4,2,3,1]`
- `chosenColors = [1,4,3,2]`

We must now verify what food & color values are assigned to 1, 2, 3, and 4. To do this, I found the `colors` and `foods` arrays in IDA by double-clicking on them in the `main` function.
![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/471583d8-e111-4b74-b1ce-553c5db22b60)
I then set a breakpoint at the if statement in the `check` function and inspected memory at `chosenColors[0]` and `chosenFoods[0]`. I had previously inputted the first item I saw in the aforementioned `colors` and `foods` arrays for Alice (the first person asked about).
Both `chosenColors[0]` and `chosenFoods[0]` were set to `1`. Doing the same for the second item and second person, I noticed they were both set to `2`. This allowed me to connect the foods to the array of integers we made above.
![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/a65760f1-6e7f-4828-9c58-c2f1fc68c4c4)
And we got the correct solution! 

