# JavaScript Questions

This is a growing collection of JavaScript snippets to ask "advanced" interviewees what the result is.

Feel free to submit pull requests :)

## Questions

Q. What's the result?

```javascript
(function() {}
    var foo = ["a","b","c","d"]
    var bar = ["z","y","x"]
    foo.splice.apply(foo, [2, 1].concat(bar));
    return foo;
})();
```

A.

```javascript
["a", "b", "z", "y", "x", "d"]
```

Q. What's the result?

```javascript
(function() {
    return (function (a, b) {}).length;
})();
```

A.

```javascript
2
```

Q. What's the result?

```javascript
(functino() {
    return NaN !== NaN;
})();
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(functino() {
    var foo = new Object();
    var bar = new Object();
    var map = new Object();

    map[foo] = "foo";
    map[bar] = "bar";

    return map[foo];
})();
```

A.

```javascript
"bar"
```

Q. What's the result?

```javascript
(function() {
    function foo() {
        return "a";
    }

    return foo();

    function foo() {
        return "b";
    }
})();
```

A.

```javascript
"b"
```

Q. What's the result?

```javascript
(function(limit) {
  for (var i = 0; i < limit; i++) {
    setTimeout(function() {
      console.log(i);
    }, 0);
  }
})(3);
```

A.

```javascript
3
3
3
```

Q. What's the result?

```javascript
(function(num) {
    return ~~num;
})(1.5);
```

A.

```javascript
1
```

Q. What's the result?

```javascript
(function(foo) {
    return !!foo
})("a");
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    return typeof null === 'object';
})();
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    this.bar = "a";

    function qux(bar) {
        this.bar = this.bar || bar;
    }

    function foo(bar) {
        return this.bar || bar;
    }

    return (function(bar) {
        return foo.bind(this)(bar);
    }).call(new qux("b"), "c");
})();
```

A.

```javascript
"b"
```

Q. What's the result?

```javascript
(functino() {
    return +(new Date())
})();
```

A.

```javascript
1393812837139
```

Q. What's the result?

```javascript
(functino() {
    return (new Date()).toString();
})();
```

A.

```javascript
"Sun Mar 02 2014 18:14:01 GMT-0800 (PST)"
```

Q. What's the result?

```javascript
(functino() {
    return (new Date()).valueOf();
})();
```

A.

```javascript
1393812845834
```

Q. What's the result?

```javascript
(function() {
    var foo = "a";
    (function(foo) {
        foo = "b";
    })(foo);
    return foo;
})();
```

A.

```javascript
"a"
```

Q. What's the result?

```javascript
(function() {
    return arguments.toString();
})();
```

A.

```javascript
"[object Arguments]"
```

Q. What's the result? (assuming window scope)

```javascript
var declared = 1;
Object.getOwnPropertyDescriptor(window, 'declared').configurable;
```

A.

```javascript
false
```

Q. What's the result? (assuming window scope)

```javascript
declared = 1;
Object.getOwnPropertyDescriptor(window, 'declared').configurable;
```

A.

```javascript
true
```

Q. What's the result?

```javascript
(function() {
    function Foo() {}

    function Bar() {}
    Bar.prototype.constructor = Bar;

    Bar.prototype = new Foo();

    return (new Bar()).constructor;
})()
```

A.

```javascript
function Foo() {}
```

## License

Released under the MIT License.
