# `luhn-number`

The Luhn test is used by some credit card companies to distinguish valid credit card numbers from what could be a random selection of digits.

A Luhn number is a sequence of digits that passes the following test:

1. Reverse the order of the digits.
2. Take the first, third, and every odd-numbered digit in the reversed digits and sum them to form `s1`
3. Taking the second, fourth, and every even-numbered digit in the reversed digits:
     1. Multiply each by two. Within each doubled digit, sum those digits (if the answer is greater than nine) to form partial sums.
     2. Sum the partial sums of the even digits to form `s2`
4. If `s1 + s2` ends in zero then the original number is in the form of a valid credit card number as verified by the Luhn test.

For example, if the trial number is 49927398716:

```
Reverse the digits:
  61789372994
Sum the odd digits:
  6 + 7 + 9 + 7 + 9 + 4 = 42 = s1
The even digits:
    1,  8,  3,  2,  9
  Two times each even digit:
    2, 16,  6,  4, 18
  Sum the digits of each multiplication:
    2,  7,  6,  4,  9
  Sum the last:
    2 + 7 + 6 + 4 + 9 = 28 = s2

s1 + s2 = 70 ends in zero, which means that 49927398716 passes the Luhn test
```

Your task for this challenge is as follows. First you will write a library file `lib/luhn-number` with a core containing an arm named `++validate`. `validate` will be a gate that takes as input a `tape` which is a sequence of digits, and returns either a `%.y` or `%.n` if the number is a Luhn number or not. 

Example usage:
```
> =ln -build-file %/lib/luhn-number/hoon
> (validate:ln "49927398716")
%.y
> (validate:ln "1234")
%.n
```

Next you will write a generator file `gen/luhn-number` which takes as input a `tape` which consists of digits or the `*` character, such as:
```
"*1*25**574*18403"
"****"
"584"
```

It will return a `(list tape)` which contains all of the Luhn numbers that fit that format. The numbers should be in lexicographic order (smallest to largest by first digit, then second digit, and so on). You may choose to import and use your `++validate` arm, or perhaps use some other strategy.

Example usage:
```
> +luhn-number "**123"
["01123" "15123" "20123" "39123" "44123" "58123" "63123" "77123" "82123" "96123" ~]

> +luhn-number "123"
~

> +luhn-number "49927398716"
[49927398716 ~]
```

Some notes: 
* We take the input as a `tape` rather than a `@ud` because a potential credit card number can have leading zeros.

* Note that in Hoon, we index starting from 0 -- so the first digit will be in the 0th index, second in 1st index, and so on.

* This website may be of use for both checking if a number is Luhn and generating a list from missing digits: https://www.dcode.fr/luhn-algorithm

* Don't worry about numbers with less than 2 digits, or improperly formatted input (with letters and spaces etc.). You can assume that the input tape will have the correct format.

Two winners will be rewarded -- one for fastest solution, and one for best style (clear, elegant, well-commented, Hoonish). For style reference, you can see [previous winners](https://developers.urbit.org/blog/hsl-competition) and the [Hoon style guide](https://developers.urbit.org/reference/hoon/style).


For submission, fill out this [google form](https://forms.gle/7JrK5f11XDYRro8t9) with your information. See instructions to create the repository below. Remember to make your repo private and add tamlut-modnys as a collaborator.

This final challenge opens at noon EST on June 17, and will close at ~11:55 AM EST on June 24. Good luck!


## Using this Repository

**Please _do not fork this repository directly on GitHub._**  Instead, please use GitHub's "template" function following [the instructions below](#creating-a-repository) to copy this repository and customize it for your project.

If you are working with a fakeship, this is one way to set things up for rapid development:

1. Start a fakeship and `|mount %base`.
2. Clone this repo into the same directory as the fakeship, then copy the contents of `src/` into `zod/base/`.
3. Develop either in `zod/base/` or in this repo folder directly.  It's probably a bit easier to develop in the fakeship and copy back here frequently.

## Testing

This repo provides test cases you can use to verify that your code submission works correctly.

To run the tests, make sure you have mounted and committed the files into the `base` folder of your fake ship. Then from dojo run
```
-test %/tests/luhn-number/hoon
```
This will run several tests, each of which will pass or fail. For debugging help you can inspect the test code to see which ones passed and failed.

To avoid issues, make sure your generator is written in the provided file at `/gen/luhn-number.hoon`, and your library file is in `/lib/luhn-number.hoon`.

For more info on testing in Hoon, see this link: https://developers.urbit.org/guides/additional/unit-tests

## Creating a Repository

1.  Log in to GitHub.
    (If you do not have an account, you can quickly create one for free.)
    You must be logged in for the remaining steps to work.

2.  On this page, click on the green "Use this template" button (top right)

3.  Select the owner for your new repository.
    (This will probably be you, but may instead be an organization you belong to.)

4.  Choose a name for your copy of the archetype repository.
    We recommend you call it `hsl-luhn-number` (no 'template').

5.  Make sure the repository is **private**, leave "Include all branches" unchecked, and click on "Create repository from template". You will be redirected to your new copy of the template respository.

6.  Share the repo with tamlut-modnys on Github as a collaborator.

After this is complete, you can use this repo to handle your competition development and submission. Please note that by submitting a solution, you allow it to be made public under the MIT license.
