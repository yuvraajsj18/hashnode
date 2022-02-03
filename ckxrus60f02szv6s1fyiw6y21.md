## How I Solved Integer to Roman Problem on Leetcode (Python)

## Problem

The problem is simple to understand, we are given an integer and we need to convert it into a Roman numeral.

**Difficulty**: Medium

Roman numerals are represented by seven different symbols: I, V, X, L, C, D, and M.

**Conversion Table**

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written from largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

- I can be placed before V (5) and X (10) to make 4 and 9. 
- X can be placed before L (50) and C (100) to make 40 and 90. 
- C can be placed before D (500) and M (1000) to make 400 and 900.

**Given an integer, convert it to a roman numeral.**

## Example

#### Example 1:

```
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
``` 

#### Example 2:
```
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

#### Example 3:
```
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Constraints

- `1 <= num <= 3999`

## Solution Template

```
class Solution:
    def intToRoman(self, num: int) -> str:
        pass  # Write your solution here
```

We have to implement the `intToRoman` function that accepts a `num` integer and returns `str`.

## Finding the Solution

### First Thought

On reading the question, the first thing that came to my mind was the solution must involve some repeated division and modulus. 
Why?
Check out the following figure:

![convert 12 to Roman numeral illustration](https://cdn.hashnode.com/res/hashnode/image/upload/v1640786210361/PCl6DILNe.png)

Let's understand, what does this image means.
We have to convert 12 to its Roman numeral equivalent. Firstly, we selected the biggest number that is smaller than 12 and whose conversion is already present in the table given above. 
That is the number 10. We divided 12 by 10 and the quotient is how many times we need to repeat 10 to get as close to 12 as possible (In our case, it is just 1).
Now, we repeat the same process for what remains that is the remainder.
Until we got 0, then we add all the strings to get the final roman numeral.

**Algorithm:**
1. Let `roman` be the final result we want. Set `roman = ""`.
2. Find the biggest small number in the conversion table than `num`. Name it `base_value`. 
3. Divide `num` by `base_value`.
4. `roman` += Roman Numeral for Base Value * Quotient.
5. Repeat steps 2 to 4 for the remainder until the remainder becomes 0.

Also make sure that:
- If the number is 0, then directly return the empty string `""` (There is no zero in Roman numerals).
- If the number is present in the conversion table, directly return the corresponding value. For example, return `X` for 10.

## Implementing the Recursive Solution

Let's now implement the solution. Start by creating a dictionary for the conversion table:

```
conversion_table = {
            1:      "I",
            5:      "V",
            10:     "X",
            50:     "L",
            100:    "C",
            500:    "D",
            1000:   "M",
            4:      "IV",
            9:      "IX",
            40:     "XL",
            90:     "XC",
            400:    "CD",
            900:    "CM",
        }
```
**Notice**, we are also including the conversions for exceptional numbers like 4, 9, 40, 90, and so on. 

Now, handle the base cases:
```
if num == 0:
    return ""

if num in conversion_table:
    return conversion_table[num]
``` 

Now, we will find the `base_value`, which is the biggest smaller value than the `num`:
```
base_value = 0
for value in conversion_table:
    if base_value < value < num:
        base_value = value
```

Now, just add a recursive call with the formula we constructed before:
```
return ((num // base_value) * conversion_table[base_value]) + self.intToRoman(num % base_value)
```

### Complete Recursive Solution Code
```
class Solution:
    def intToRoman(self, num: int) -> str:
        conversion_table = {
            1:      "I",
            5:      "V",
            10:     "X",
            50:     "L",
            100:    "C",
            500:    "D",
            1000:   "M",
            4:      "IV",
            9:      "IX",
            40:     "XL",
            90:     "XC",
            400:    "CD",
            900:    "CM",
        }

        if num == 0:
            return ""

        if num in conversion_table:
            return conversion_table[num]
        
        # base_value = biggest smaller value than num
        base_value = 0
        for value in conversion_table:
            if base_value < value < num:
                base_value = value

        return ((num // base_value) * conversion_table[base_value]) + self.intToRoman(num % base_value)
```

### Output
```
>>> Solution().intToRoman(12)
>>> `XII`
>>> Solution().intToRoman(1234)
>>> `MCCXXXIV`
```

## Non-Recursive Solution (Using a While Loop)

Here's a non-recursive solution using the same algorithm:
```
class Solution:
    def intToRoman(self, num: int) -> str:
        conversion_table = {
            1:      "I",
            5:      "V",
            10:     "X",
            50:     "L",
            100:    "C",
            500:    "D",
            1000:   "M",
            4:      "IV",
            9:      "IX",
            40:     "XL",
            90:     "XC",
            400:    "CD",
            900:    "CM",
        }
        
        
        roman = ""    
            
        while num:
            
            if num == 0:
                return roman
        
            if num in conversion_table:
                return roman + conversion_table[num]

            
            base_value = 0
            for value in conversion_table:
                if base_value < value < num:
                    base_value = value
            
            roman += ((num // base_value) * conversion_table[base_value])
            num = num % base_value
    
        
        return  roman 
```

## Result

The solution is accepted on Leetcode:

![result](https://cdn.hashnode.com/res/hashnode/image/upload/v1640799638452/Gb5nJLzuZ.png)


## Try it Out

<iframe style='max-width:100%; border: none' height=375 width=700 src=https://www.interviewbit.com/embed/snippet/c17de0136e0c0275450a title='Interviewbit Ide snippet/c17de0136e0c0275450a' loading="lazy" allow="clipboard-write" allowfullscreen/>

## Conclusion

- We converted an integer to a roman numeral using a recursive and a non-recursive solution.
- We developed the algorithm using the division and modulus operator.

Note: This is not supposed to be the "best" solution to this problem. This is just what I thought of. 
If you have a better solution or some feedback to improve this solution, please let me know in the comments.

Like and follow for more such articles.
Connect with me on [Twitter](https://twitter.com/yuvraajsj18), [GitHub](https://github.com/yuvraajsj18), and [LinkedIn](https://www.linkedin.com/in/yuvraajsj18/).



