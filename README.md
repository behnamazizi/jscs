# JavaScript Code Snippets

### Calculate Factorial of Number
```javascript

function factorialize(num) {
  return num < 0 ? -1 : num == 0 ? 1 : num * factorialize(num - 1);
}

factorialize(7);
//  expected output: 7
```

### Calculate Probability of Combinations
```javascript
// Number of sample points in set (n)	
// Number of sample points in each combination (r)	

function probabilityOfCombinations(n, r) {
  return factorialize(n) / (factorialize(r) * factorialize(n - r));
}

probabilityOfCombinations(10, 3);
// expected output: 120

```
