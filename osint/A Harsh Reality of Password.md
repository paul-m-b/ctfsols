# A Harsh Reality of Passwords

Challenge description:
```
Recently, Iris's company had a breach. Her password's hash has been exposed. This challenge is focused on understanding Iris as a person.

 

Hash: $2b$04$DkQOnBXHNLw2cnsmSEdM0uyN3NHLUb9I5IIUF3akpLwoy7dlhgyEC

The flag format is irisctf{plaintextPassword}

Note:

Hi everyone, here are hints for the last osint challenge with the password hash.

Focus on Iris and what she finds important!

There are three words (not letters, but words), and a certain amount of numbers following it

There's no leet words, proper capitalization nothing like (ExAmPLE), no special characters as well like -,! etc.

If you find a specific date, do not include the month'a name into your word list. Just use the numbers!!
```

We're given a hash and layout of Iris' password. In order to solve this we need to construct a wordlist of everything she finds important. We can also assume that the "numbers" at the end of the password are some sort
of date. Since the challenge says to focus on Iris, I decided to look over her Instagram in order to make a wordlist of stuff she says is important. This is the list I created:

```
    "Mimosas",
    "Portofino",
    "Tiramisu",
    "Mom",
    "Italy",
    "Amsterdam",
    "Swans",
    "Europe",
    "Milan",
    "Netherland",
    "Berlin",
    "Starbucks",
    "April"
```

(note: "Proper capitalization" in the hint means that each word is capitalized as if it were the first word in a sentence.)

She also specifically says that her Mom's birthday is an important date. So, I also made a numbers list: `["04","8","1965"]` (found from her mom's facebook page, which was found in the "Personal Breach" challenge).
But, because her own birthday is probably important to her as well, I decided to add it in: `["04","8","1965","27","4"]` and I put the non-zero-padded 4 as well just to be safe. 

The last thing we needed to do before cracking the hash is figuring out what kind of hash it actually was. I used hashcat and a couple of online tools to verify that it was a `Bcrypt` hash.

Then, I made a Python script (credit chatGPT) to find all three word combinations in my wordlist and three number combinations in my number list. Hashcat or some other password cracker is almost certainly a more efficient
way to solve this problem, but I landed on a python script and stuck with it.

```python
from itertools import product
import bcrypt

def generate_combinations(words, numbers):
    combinations = []
    for word_combo in product(words, repeat=3):
        for num_combo in product(numbers, repeat=3):
            word_str = ''.join(word_combo)
            num_str = ''.join(num_combo)

            check = f"{word_str}{num_str}"
            checkbytes = check.encode("utf-8")

            print(f"Checking: {check}")
            result = bcrypt.checkpw(checkbytes, b"$2b$04$DkQOnBXHNLw2cnsmSEdM0uyN3NHLUb9I5IIUF3akpLwoy7dlhgyEC")
            if result:
                print("FOUND")
                print(check)
                return

wordlist = [
    "Mimosas",
    "Portofino",
    "Tiramisu",
    "Mom",
    "Italy",
    "Amsterdam",
    "Swans",
    "Europe",
    "Milan",
    "Netherland",
    "Berlin",
    "Starbucks",
    "April"
]


wordlist += capitalized_wordlist

number_set = ['04', '1996', '27','8','1965','4']

all_combinations = generate_combinations(wordlist, number_set)
```

The script found that the password `PortofinoItalyTiramisu0481965` matched the provided hash. So all we had to do is wrap that in `irisctf{}` and submit the flag!
