# JavaScript Code Snippets

### Calculate Factorial of Number
```javascript

function factorialize(num) {
  return num < 0 ? -1 : num == 0 ? 1 : num * factorialize(num - 1);
}

factorialize(7);
//7

```
