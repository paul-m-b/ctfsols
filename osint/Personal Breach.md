# Personal Breach
In this challenge, we need to find three pieces of information about Iris. Her age, the hospital she was born, and where she works.

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/5019eec0-59d1-49a7-822e-2598d5164cae)

I started off at Michelangelo Corning's instagram page (which was found as part of the previous OSINT challenge, "Away on Vacation"). I immediately looked at the people he is following.

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/548651b5-75ee-43d3-bc11-fddff7eb3faf)

Iris Stein is one of them! Maybe she has some information on her instagram. I clicked through Iris's posts but didn't find any answers to our questions. But, one post made mention to her mother and gave an @.

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/04e70fca-6d91-4b59-803a-38b0c968b406)

Her mom didn't want to get Instagram, but she definitely has some sort of social media. For no reason at all, I immediately thought that Facebook would likely be her mom's social media of choice.

There are a couple of results for "Elaina Stein" on facebook, but this profile was clearly related to the challenge. https://www.facebook.com/profile.php?id=61555040318052

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/1014a891-1da8-45bf-892a-9e54cc6aba15)

Looks like we found Iris's birthday! `April 27th, 1996` makes her 27 years old. We have our first answer. This also leads us directly to the second answer, her birth hospital. I scrolled down to find a post related to Iris'
birthday and I found the following: 

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/3a8440d9-e281-44bc-852a-777daa31f564)

Doing a reverse image search of the picture in the post reveals:

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/1a648f1b-cb51-4fef-94b2-97ba727ff8fc)

`Lenox Hill Hospital` our second answer!

Now, to find where she works. I went to LinkedIn and searched Iris Stein. There were again, a few results. But, from the "Away on Vacation" challenge we know that Iris works in HR:

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/8e371fb8-ed26-4599-946f-9fa746a683b8)

And we have our third answer! `Mountain Peak Hiring Agency`

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/3e1e1860-e799-4642-845e-32af8a4e7072)
