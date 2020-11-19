# JavaScript Code Snippets

## Table of Contents
| No. | Questions |
|---- | ---------
|1  | [Generate a random number in a given range](#How-to-generate-a-random-number-in-a-given-range) |
|2  | [Find the difference between two arrays](#How-to-find-the-difference-between-two-arrays)|

**[⬆ Back to Top](#table-of-contents)**
### How to generate a random number in a given range
```javascript
// Returns a random number(float) between min (inclusive) and max (exclusive) 

const getRandomNumber = (min, max) => Math.random() * (max - min) + min;

getRandomNumber(2, 10)

 // Returns a random number(int) between min (inclusive) and max (inclusive)

const getRandomNumberInclusive =(min, max)=> {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

getRandomNumberInclusive(2, 10);
```
