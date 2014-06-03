promise-mock
============

A mock for [native style](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) promises.


How to use in Node.js
=====================

This lib will mock native style promises. It takes the Promise constructor as an argument.
In node, it's best to use a module such as [then/promise](https://github.com/then/promise).

Given a jasmine test runner, an example of using this lib looks like:

```javascript
  var Promise = require('promise');
  var promiseMock = require('promise-mock');

  describe('promise mock demo', function () {
  
    var MockedPromise;
    
    beforeEach(function () {
      MockedPromise = promiseMock.getMock(Promise);
    });
    
    it('should make promises synchronous', function () {
      var number = 1;
    
      var mockedPromise = new MockedPromise(function (resolve, reject) {
        resolve(number);
      });
      
      mockedPromise.then(function (number) {
        return ++number;
      });
      
      promiseMock.flush(); // flushes all promises.
      // could also do:
      // mockPromise.flush();
      // promiseMock.flush(mockPromise);
      // promiseMock.flush(1);
      
      expect(number).toBe(2);
    });
    
    
    afterEach(function () {
      promiseMock.restore();
    });
  });
```
