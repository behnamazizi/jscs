# JavaScript Code Snippets

## Calculate Factorial of Number
```javascript
function factorialize(num) {
  return num < 0 ? -1 : num == 0 ? 1 : num * factorialize(num - 1);
}

factorialize(7);
//  expected output: 7
```
---
## Calculate Probability of Combinations
_To calculate the factorial of a number: [factorialize(num)](#Calculate-Factorial-of-Number)_
```javascript
// Number of sample points in set (n)	
// Number of sample points in each combination (r)


function probabilityOfCombinations(n, r) {
  return factorialize(n) / (factorialize(r) * factorialize(n - r));
}

probabilityOfCombinations(10, 3);
// expected output: 120

```
## Change English Numbers to Farsi (0123456789 --> ۰۱۲۳۴۵۶۷۸۹)
```javascript
function farsiNumbers(number){
  let fn =["۰","۱","۲","۳","۴","۵","۶","۷","۸","۹"];
  return number.toString().split('').map(ch => {
    return ch.match(/[0-9]/g) ? fn[parseInt(ch)] : ch
  }).join('')
}

farsiNumbers("7 Apples Plus 5 Apple is equal to 12 Apples!");
//  expected output: "۷ Apples Plus ۵ Apple is equal to ۱۲ Apples!"

farsiNumbers(1.618);
//  expected output: "۱.۶۱۸"

```
---
