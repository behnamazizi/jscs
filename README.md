# JavaScript Code Snippets

## Table of contents
| Num | Title |
|:---:| --- |
| 1 | [Calculate Factorial of Number](#calculate-factorial-of-number) |
| 2 | [Calculate Probability of Combinations](#calculate-probability-of-combinations) |
| 3 | [Convert English Digits to Farsi](#convert-english-digits-to-farsi) |
| 4 | [Convert Arabic Characters to Farsi](#convert-arabic-characters-to-farsi) |
| 5 | [Generate a Ranged Random Number](#generate-a-ranged-random-number) |
| 6 | [Parse CSV to Object](#parse-csv-to-object) |
| 7 | [Address Object Property by String](#address-object-property-by-string) |
| 8 | [Get Number of Lines in a Paragraph](#get-number-of-lines-in-a-paragraph) |
| 9 | [Calculate Book Spine Thickness](#calculate-book-spine-thickness) |
| 10 | [2D Canvas Gradient Generator](#2d-canvas-gradient-generator) |
| 11 | [2D Canvas Round Corner Rectangle](#2d-canvas-round-corner-rectangle) |
| 12 | [Check the possibility of swipe in a 2d matrix](#Check-the-possibility-of-swipe-in-a-2d-matrix) |
| 13 | [Try Catch a Fetch](#Try-Catch-a-Fetch) |

---

### Calculate Factorial of Number

```javascript
function factorialize(num) {
  return num < 0 ? -1 : num == 0 ? 1 : num * factorialize(num - 1);
}

factorialize(7);
//  expected output: 5040
```
---
### Calculate Probability of Combinations
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
### Convert English Digits to Farsi
_(0123456789 --> ۰۱۲۳۴۵۶۷۸۹)_
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
### Convert Arabic Characters to Farsi
_(ي ك ة ٤ ٥ ٦ --> ی ک ه ۴ ۵ ۶)_
```javascript
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
### Generate a Ranged Random Number
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
### Parse CSV to Object
```javascript
const myCSV = `id,first name,last name,address,city,age
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

csvToObject(myCSV, true);
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
csvToObject(myCSV, false);
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

### Address Object Property by String

```javascript
myObject = { A : { B: { C: [{ value: 'Brenda' }, { value: 'Jim' }, { value: 'Lucy' }] } }};

function getValue(o, path) {
    return path.replace(/\[/g, '.').replace(/\]/g, '').split('.').reduce((acc, cur) => {
        return (acc || {})[cur];
    }, o);
}

getValue(myObject , 'A.B.C 1 d[2]')
//expected output: {value: "Lucy"}
```

---

### Get Number of Lines in a Paragraph

```javascript
function countLines(el) {
    let style = window.getComputedStyle(el, null);
    let height = parseInt(style.getPropertyValue('height'));
    let lineHeight = parseInt(style.getPropertyValue('line-height'));
    return Math.ceil(height / lineHeight);
}
```

---

### Calculate Book Spine Thickness

```javascript
function spine(paperweight, papervolume, numberofpages, typeofcover) {
    const volume = {
            "gloss": 8,
            "satin": 9,
            "matt": 9,
            "silk": 9,
            "mattBulk": 11,
            "uncoated": 12.5,
            "bookWove": 12.5,
            "bookWoveCream": 18
        },
        cover = {
            "hardback": 6,
            "paperback": 1
        }
    return ((paperweight * volume[papervolume] * numberofpages) / 20000) + cover[typeofcover];
}

spine(80, "uncoated", 120, "hardback");
//expected output: 12
```

---

### 2D Canvas Gradient Generator

```javascript
function lineGradient(ctx, sx, sy, ex, ey, colors) {
    let gradient = ctx.createLinearGradient(sx, sy, ex, ey);
    colors.forEach((color, i) => {
        gradient.addColorStop(color[0], color[1]);
    })
    return gradient
}

lineGradient(ctx, 0, 0, 100, 100, [[0,"red"],[1,"blue"]]);
```

```javascript
function radialGradient(ctx, x0, y0, r0, x1, y1, r1, colors) {
    let gradient = ctx.createRadialGradient(x0, y0, r0, x1, y1, r1);
    colors.forEach((color, i) => {
        gradient.addColorStop(color[0], color[1]);
    })
    return gradient
}

radialGradient(ctx, 100, 100, 0, 100, 100, 50, [[0,"red"],[1,"blue"]])
```

---

### 2D Canvas Round Corner Rectangle
```javascript
function roundRectangle(x, y, w, h, r) {
    r = typeof r == "object" ? r : [r,r,r,r];
    let path = new Path2D();
    path.moveTo(x, y + r[0]);
    path.arcTo(x, y, x + r[0], y, r[0]);
    path.arcTo(x + w, y, x + w, y + r[1], r[1]);
    path.arcTo(x + w, y + h, x + w - r[2], y + h, r[2]);
    path.arcTo(x, y + h, x, y + h - r[3], r[3]);
    return path;
}

```
---

### Check the possibility of swipe in a 2d matrix
this function checks if two member of a 2d matrix are swipeable by checking that they are in same row or column and they are neighbors.

```javascript
function isPossible(array,a,b){
    let rowA = Math.floor(array.flat().indexOf(a) / array[0].length),
        colA = array[rowA].indexOf(a);
    let rowB = Math.floor(array.flat().indexOf(b) / array[0].length),
        colB = array[rowB].indexOf(b);
    return rowA == rowB && Math.abs(colA - colB) == 1 ? true : colA == colB && Math.abs(rowA - rowB) == 1 ? true : false;
}

// sample matrix:
matrix = [
    [1, 2, 3, 4, 5],
    [6, 7, 8, 9, 10],
    [11, 12, 13, 14, 15],
]

isPossible(matrix,3,8)
//expected output: true
isPossible(matrix,3,13)
//expected output: false
```
---

### Try Catch a Fetch

```javascript
fetch(url).then((response) => {
  if (response.ok) {
    return response.json();
  }
  throw new Error('Something went wrong');
})
.then((responseJson) => {
  // Do something with the response
})
.catch((error) => {
  console.log(error)
});

```