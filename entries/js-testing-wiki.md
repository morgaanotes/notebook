# Javascript testing wiki

## Mocha

### Run only one test suite without `.only`

```
mocha --grep api
```

This will run the test suite described as below:

```js
describe('api', _ => {
  // ...
})
```
