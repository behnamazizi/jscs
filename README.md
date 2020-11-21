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
---
## Convert English Digits to Farsi (0123456789 --> ۰۱۲۳۴۵۶۷۸۹)
```javascript
function farsiDigits(number){
  return number.toString().split('').map(ch => {
    return ch.match(/[0-9]/) ? ["۰","۱","۲","۳","۴","۵","۶","۷","۸","۹"][parseInt(ch)] : ch
  }).join('')
}

farsiDigits("7 Apples Plus 5 Apple is equal to 12 Apples!");
//  expected output: "۷ Apples Plus ۵ Apple is equal to ۱۲ Apples!"

farsiDigits(1.618);
//  expected output: "۱.۶۱۸"

```
---
## Convert Arabic Characters to Farsi (ي ك ة ٤ ٥ ٦ --> ی ک ه ۴ ۵ ۶)
```
function persianizer(text){
  return text.toString().split('').map(ch => {
    let ar = ["ي","ك","ة","٤","٥","٦"].indexOf(ch);
    let fa = ["ی","ک","ه","۴","۵","۶"];
    return ar > -1 ? fa[ar] : ch
  }).join('')
}

persianizer("كة ٥ تا بستة نمونة كوچك از فرداي كودك و ٦٤٥ تك تك مي‌شود.")
//  expected output:  'که ۵ تا بسته نمونه کوچک از فردای کودک و ۶۴۵ تک تک می‌شود.'
```
---
## Generate a Ranged Random Number
```javascript
function getRandomInt(min, max, decimal) {
  min = decimal ? Math.ceil(min) : min;
  max = decimal ? Math.floor(max) : max;
  let rnd = Math.random() * (max - min) + min;
  return decimal ? rnd  : Math.floor(rnd);
}

getRandomInt(1, 3, true);
//  expected output: 1.0 to 3.0

getRandomInt(1, 3, false);
//  expected output: 1 or 2 or 3
```
---
## Parse CSV to Object
```javascript
const SapmpleCSV = `id,first name,last name,address,city,age
569874,John,Doe,120 jefferson st.,Riverside,32
254789,Jack,McGinnis,220 hobo Av.,Phila,22
214778,John,Repici,120 Jefferson St.,Riverside,24
458718,Stephen,Tyler,7452 Terrace road,SomeTown,28
366987,Joan,Jet,9th, at Terrace plc,Desert City,33`;

function csvToObject(csv, header) {
  let arr = [];
  let hdr = header ? csv.split('\n')[0].split(',') : null;
  csv.split('\n').forEach((row, index) => {
    row = row.split(',');
    if (header && index > 0) {
      ro = {};
      hdr.forEach((title, no) => {
        ro[title.replace(/\s/g, '')] = row[no];
      });
      arr.push(ro)
    }else if(!header){
      arr.push(row)
    }
  });
  return arr;
}

csvToObject(SapmpleCSV, true);
/*
expected output:
[
  {
    id: '569874',
    firstname: 'John',
    lastname: 'Doe',
    address: '120 jefferson st.',
    city: 'Riverside',
    age: '32'
  },
  {
    id: '254789',
    firstname: 'Jack',
    lastname: 'McGinnis',
    address: '220 hobo Av.',
    city: 'Phila',
    age: '22'
  },
  ...
  ]
*/
csvToObject(SapmpleCSV, false);
/*
expected output:
[
  [ 'id', 'first name', 'last name', 'address', 'city', 'age' ],
  [ '569874', 'John', 'Doe', '120 jefferson st.', 'Riverside', '32' ],
  [ '254789', 'Jack', 'McGinnis', '220 hobo Av.', 'Phila', '22' ],
  ...
  ]
*/
```
---







