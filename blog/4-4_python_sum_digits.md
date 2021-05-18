---
slug: python_sum_digits
title: Python 3 - Sum of the Digits of Positive Integers
date: April 4, 2021
author: Pranav Ramesh
author_title: Technepreneur & blogger
author_url: https://github.com/pr28416
author_image_url: https://media-exp1.licdn.com/dms/image/C4D03AQE8US7zv3uUhQ/profile-displayphoto-shrink_400_400/0/1619024957277?e=1626912000&v=beta&t=cDgil4bLuNR5N8cVLnZHlmfiHcZ_ad0HKC2KsPbONfM
tags: [python]
---

Suppose we are given a positive integer, and we want to find the sum of its digits and return it to the user. For instance, the sum of the digits of 12345 should yield 15  because 1 + 2 + 3 + 4 + 5 = 15.

To begin, we know that we need to be able to acquire each digit of our number. We can acknowledge that the order in which we acquire each digit doesn't matter, because we will still receive the same sum. For instance, if we wanted the sum of the digits of 12345, it wouldn't matter whether we added 1 + 2 + 3 + 4 + 5 or 5 + 4 + 3 + 2 + 1, as both sums simplify to 15.

We can use this fact to our advantage. We must first identify how to acquire each digit of our number. We have two options: get the digits from left to right, or from right to left. The left-to-right approach is more complex, so we will take the right-to-left approach.

Taking 12345 as our example, we know that the units digit, 5, is five away from a multiple of ten, 12340. This means that we can take 12345 mod 10 to get 5, which is our units digit. This operation will work in all situations. For instance, 1234 mod 10 is 4, and 432 mod 10 is 2.

After we take our number mod 10, we must be able to repeat the same process with the digit after the units digit. This means that we have to remove the current units digit, 5, from 12345. In order to do that, we can floor-divide by 10, meaning that we round down the quotient of 12345/10 = 1234.5, or 1234.

Therefore, our two steps are:
Add the result of our number mod 10 to a sum variable.
Remove the units digit from the number by floor-dividing the number by 10.
​
We will keep repeating these two steps until the number is 0, because at that point, there are no more digits to extract. We also know that we will always be able to stop at 0, because we will eventually end up with a single digit as our number, and floor dividing a single digit by 10 (e.g. 7 / 10) yields 0.

We can begin by writing our function header with the identifier `sumDigits` and a single parameter, `num​`.

```python title="Define sumDigits()"
def sumDigits(num):
    pass # Code will follow
```

Next, we need to be able to keep track of our current sum, so we should create a `​totalSum​` variable.

```python title="Create totalSum variable"
def sumDigits(num):
    totalSum = 0
```

Now, we need to write our loop header. Because we don't know at what point we will reach 0, we will use a `while` loop, where the condition is `num > 0`​.

```python title="Write a while loop"
def sumDigits(num):
    totalSum = 0
    while num > 0:
        pass # Code will follow
```

At this point, inside the while​ loop, we can perform our two iterative steps of adding the units digit to totalSum and removing the units digit from the number.

```python title="Performing math operations"
def sumDigits(num):
    totalSum = 0
    while num > 0:
        totalSum += num % 10
        num //= 10
```

Finally, after the loop ends, we can return the total sum.

```python title="Return total sum"
def sumDigits(num):
    totalSum = 0
    while num > 0:
        totalSum += num % 10
        num //= 10
    return totalSum
```

Our function is now finished, and we can test it with various inputs.