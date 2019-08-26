# Javascript testing wiki

## Terminology

- Unit Tests:Testing individual functions.
- Integration Tests: Testing the combination of various functions or modules.
- End to End Tests: Sometimes referred to as functional tests, testing actual user flows through your application.
- Quality Assurance (QA) Testing: Testing to verify that the functionality meets requirements.
- User Acceptance Testing (UAT): Testing to receive validation from stakeholders that the functionality meets requirements.


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
