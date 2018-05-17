---
title: "Challenges"
date: 2018-04-25T13:28:03+11:00
draft: false
---
# 27 Apr 2018

### Challenge 1: Vowel Count

This problem is to get us introduced to string processing. We will be given several lines of text - and for each of them we want to know the number of vowels (i.e. letters `a, o, u, i, e, y`). Note: that `y` is regarded as a vowel for purpose of this task.

* Each line in the input data file is a test case.
* The lines consist only of lowercase English (Latin) letters and spaces.
* The answer should contain the number of vowels in each line, separated by spaces.

For example:

```
input data:

abracadabra

pear tree

o a kak ushakov lil vo kashu kakao

my pyx

answer:
5 4 13 2

```

* [Download the test data here](april_27_challenge_one_test_data.txt)

This [challenge is originally from codeabbey and can be found here.](http://www.codeabbey.com/index/task_view/vowel-count)

### Challenge 2: Rotate string

To rotate strings by K characters means to cut these characters from the beginning and transfer them to the end. If K is negative, characters, on contrary should be transferred from the end to the beginning.

* Each line in the input data file will contain a number `K` and some string `S` separated by space - one pair in each line.
* String `S` will contain only small latin letters. `K` will not exceed half the length of `S` by absolute value.
* The answer should contain strings rotated in accordance with the rule above, separated by spaces. 

For example:

```
input data:

3 forwhomthebelltolls

-6 verycomplexnumber

answer:

whomthebelltollsfor numberverycomplex

```

* [Download the test data for the challenge here](april_27_challenge_two_test_data.txt)

This challenge is [originally from codeabbey and can be found here.](http://www.codeabbey.com/index/task_view/rotate-string)

### Challenge Three: Anagrams

In many natural languages we can find some pairs of words which could be transformed to each other by changing the order of letters. I.e. they consist of the same set of letters, for example:

cat - act, take - teak, ate - eat - tea

Such words are called anagrams and as we see in the third example sometimes there are more than two words.

Your task is to find out the amount of anagrams for a given word in the dictionary.

[Download the dictionary file](april_27_dictionary.txt)

*(This dictionary file contains a list of english words, one per line. It was taken from Ubuntu linux distribution and stripped of words containing capital letters, apostrophes and non-english letters.)*

* Each line in the input data file will contain a single word.
* The answer should contain the number of anagrams for each word (not including the word itself).

For example:

```
input data:

bat

coal

lots

answer:
1 1 2

```

[Download the test data](april_27_challenge_three_test_data.txt)

This challenge is [originally from codeabbey and can be found here.](http://www.codeabbey.com/index/task_view/anagrams)


### Visualisation Challenge:

Since difficulties in processing household recycling waste have been in the news lately, the Victorian Local Government Waste Services Report 2015-16 make for a topical dataset.

Report: http://www.sustainability.vic.gov.au/Government/Victorian-Waste-data-portal/Victorian-Local-Government-Annual-Waste-Services-report

Data: http://www.sustainability.vic.gov.au/-/media/SV/Publications/Government/Victorian-waste-data-portal/Victorian-Local-Government-Annuals-Waste-Services-report/Victorian-Local-Government-Waste-Services-Report-Workbook-201516.xlsx

For this data fluency challenge; lets visualise how has waste composition and processing changed from 2001-2014, (Data in ‘Key time series tables.’ tab). You could make a static graph, interactive plot or anything you like. 

Additionally - are there any interesting insights to be made from the other data in this document?

We can share our different approaches on the day.
