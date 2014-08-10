# JavaScript Idiosyncrasies

This is a growing collection of JavaScript idiosyncrasies, or things that are not easily understood.

If you can explain *why* the answer is to all questions then you are truly a JavaScript ninja. Some of these are just to confuse the reader, and by no means encourage best practices and should be never be seen in production code. It's simply to demonstrate if one has a strong grasp of the language and knows what I'm trying to get at.

Feel free to submit pull requests :)

---

Q. What's the result?

```javascript
(function() {
    var foo = new Object();
    var bar = new Object();
    var map = new Object();

    map[foo] = 'foo';
    map[bar] = 'bar';

    return map[foo];
})();
```

A.

```javascript
"bar"
```

[JSBin](http://jsbin.com/xogaki/1/edit)

Q. What's the result?

```javascript
function f() {
    return 'foo';
}
(function() {
    if (1 == 0) {
        function f() {
            return 'bar';
        }
    }
    return f();
})();
```

A.

```javascript
"bar"
```

[JSBin](http://jsbin.com/lotavo/1/edit)

Q. What's the result?

```javascript
(function() {
    return NaN !== NaN;
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/katana/1/edit)

Q. What's the result?

```javascript
(function() {
    function foo() {
        return 'a';
    }

    return foo();

    function foo() {
        return 'b';
    }
})();
```

A.

```javascript
"b"
```

[JSBin](http://jsbin.com/yutuce/1/edit)

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

[JSBin](http://jsbin.com/focobo/1/edit)

Q. What's the result?

```javascript
(function(a, b) {
  arguments[1] = 3;
  return b;
})(1, 2);
```

A.

```javascript
3
```

[JSBin](http://jsbin.com/hajus/1/edit)

Q. What's the result?

```javascript
(function() {
    return ~(-3);
})();
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/begehe/1/edit)

Q. What's the result?

```javascript
(function() {
    return ~~(-3.4);
})();
```

A.

```javascript
-3
```

[JSBin](http://jsbin.com/migohi/1/edit)

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

[JSBin](http://jsbin.com/rusas/1/edit)

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

[JSBin](http://jsbin.com/roniwu/1/edit)

Q. What's the result?

```javascript
(function(x) {
    return !!x
})('a');
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/rahuy/1/edit)

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

[JSBin](http://jsbin.com/nurihe/3/edit)

Q. What's the result?

```javascript
(function() {
    this.bar = 'a';

    function qux(bar) {
        this.bar = this.bar || bar;
    }

    function foo(bar) {
        return this.bar || bar;
    }

    return (function(bar) {
        return foo.bind(this)(bar);
    }).call(new qux('b'), 'c');
})();
```

A.

```javascript
"b"
```

[JSBin](http://jsbin.com/bediq/2/edit)

Q. What's the result?

```javascript
(function() {}
    var foo = ['a','b','c','d'];
    var bar = ['z','y','x'];
    foo.splice.apply(foo, [2, 1].concat(bar));
    return foo;
})();
```

A.

```javascript
["a", "b", "z", "y", "x", "d"]
```

[JSBin](http://jsbin.com/qigub/2/edit)

Q. What's the result?

```javascript
(function() {
    return +(new Date())
})();
```

A.

```javascript
1393812837139
```

[JSBin](http://jsbin.com/lobib/2/edit)

Q. What's the result?

```javascript
(function() {
    return (new Date()).valueOf();
})();
```

A.

```javascript
1393812845834
```

[JSBin](http://jsbin.com/loxim/1/edit)

Q. What's the result?

```javascript
(function() {
    return (new Date()).toString();
})();
```

A.

```javascript
"Sun Mar 02 2014 18:14:01 GMT-0800 (PST)"
```

[JSBin](http://jsbin.com/hiheq/1/edit)

Q. What's the result?

```javascript
(function() {
    var foo = 'a';
    (function(foo) {
        foo = 'b';
    })(foo);
    return foo;
})();
```

A.

```javascript
"a"
```

[JSBin](http://jsbin.com/mifiy/1/edit)

Q. What's the result?

```
(function() {
    function foo(qux) {
        return qux || this.foo;
    }

    return (Function.bind.bind(Function.call)(foo))({foo: 'foo'}, 'qux');
})();
```

A.

```javascript
"qux"
```

[JSBin](http://jsbin.com/caruye/1/edit)

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

[JSBin](http://jsbin.com/foqoc/1/edit)

Q. What's the result?

```javascript
(function() {
    function always(val) {
        return function() {
            return val;
        };
    }

    var f = always(function(){});
    var g = always(function(){});

    return f() === g();
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/yikero/1/edit)

Q. What's the result?

```javascript
(function() {
    var num1 = 10;
    var num2 = new Number('10');
    return num1 === num2;
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/jivini/1/edit)

Q. What's the result?

```
(function() {
    return [1+1] === [2];
})()
```

A.

```
false
```

[JSbin](http://jsbin.com/nilagi/1/edit)

Q. What's the result?

```javascript
(function() {
    var obj1 = { foo: 'bar' };
    var obj2 = { foo: 'bar' };
    return obj1 === obj2;
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/dokej/1/edit)

Q. What's the result?

```javascript
(function() {
    return ['10','10','10','10'].map(parseInt);
})();
```

A.

```javascript
[10, NaN, 2, 3]
```

[JSBin](http://jsbin.com/culufi/1/edit)

Q. What's the result?

```javascript
(function() {
    var o = {
        toString: function() {
            return 'a';
        },
        valueOf: function () {
            return 1;
        }
    };

    return o+o;
})();
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/qinol/1/edit)

Q. What's the result?

```javascript
(function() {
    function Foo() {}

    function Bar() {}
    Bar.prototype.constructor = Bar;

    Bar.prototype = new Foo();

    return (new Bar()).constructor;
})();
```

A.

```javascript
function Foo() {}
```

[JSBin](http://jsbin.com/worug/1/edit)

Q. What's the result?

```javascript
(function() {

  var f = function g() {
    return 1;
  };

  return g();

})();
```

A.

```javascript
ReferenceError: g is not defined
```

[JSBin](http://jsbin.com/pibob/1/edit)

Q. What's the result?

```javascript
(function() {

  return void (1+1);

})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/cawiro/1/edit)

Q. What's the result?

```javascript
(function() {

  var a = [1,2];
  var b = a;

  a = [1,2];

  return a === b;

})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/kucob/1/edit)

Q. What's the result?

```javascript
(function() {
    return {foo: 'bar'} === {foo: 'bar'};
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/meyet/1/edit)

Q. What's the result?

```javascript
(function() {
    var questionable = 'outer';

    return (function () {
        return questionable;

        var questionable = 'inner';
    })();
})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/kesori/1/edit)

Q. What's the result?

```javascript
(function() {
    return new String('foo') === 'foo';
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/femeto/1/edit)

Q. What's the result?

```javascript
(function(n) {
    var even = function (num) {
        return (num === 0) || !(even(num - 1))
    };

    var _even = even;

    even = void 0;

    return _even(n);
})(2);
```

A.

```javascript
TypeError: undefined is not a function
```

[JSBin](http://jsbin.com/mopab/1/edit)

Q. What's the result?

```javascript
(function() {
    var n;

    function name() {
        return this.name
    };

    n = name.bind({name: 'foo'});
    n.bind({name: 'bar'})

    return n();
})();
```

A.

```javascript
"foo"
```

[JSBin](http://jsbin.com/yokaw/1/edit)

Q. What's the result?

```javascript
(function() {
    return ('3' > '12') === ('03' > '12');
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/mohuf/1/edit)

Q. What's the result?

```javascript
(function() {
    return Math.pow(2,53) === (Math.pow(2,53) + 1);
}();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/warowo/1/edit)

Q. What's the result?

```javascript
(function() {
    return Math.pow(2,1024) === Infinity;
}();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/xozim/1/edit)

Q. What's the result?

```javascript
(function() {
    return (Infinity - 100) === Infinity;
}();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/dijiqo/1/edit)

Q. What's the result?

```
(function() {
    return (0.1 + 0.2 === 0.3);
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/nedupi/1/edit)

Q. What's the result?

```
(function() {
    return parseFloat('3.3.4');
})();
```

A.

```javascript
3.3
```

[JSBin](http://jsbin.com/wuxobi/1/edit)

Q. What's the result?

```
(function() {
    return 010;
})();
```

A.

```javascript
8
```

[JSBin](http://jsbin.com/sugewu/1/edit)


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

### Weird parts of JavaScript

Q. What's the result?

```
(function() {
    return ![];
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/puyap/1/edit)

Q. What's the result?

```
(function() {
    return +[];
})();
```

A.

```javascript
0
```

[JSBin](http://jsbin.com/huboca/1/edit)

Q. What's the result?

```
(function() {
    return +[![]];
})();
```

A.

```javascript
NaN
```

[JSBin](http://jsbin.com/fusine/1/edit)

Q. What's the result?

```
(function() {
    return [][[]];
})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/vetiba/1/edit)

Q. What's the result?

```
(function() {
    return +!+[];
})();
```

A.

```javascript
1
```

[JSBin](http://jsbin.com/dulih/1/edit)

Q. What's the result?

```
(function() {
    return []+[];
})();
```

A.

```javascript
""
```

[JSBin](http://jsbin.com/lekun/1/edit)

Q. What's the result?

```
(function() {
    return true + 1;
})();
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/femicu/1/edit)

Q. What's the result?

```
(function() {
    return 0.06 + 0.01;
})();
```

A.

```javascript
0.06999999999999999
```

[JSBin](http://jsbin.com/lirac/1/edit)

Q. What's the result?

```
(function() {
    return (parseInt('10000000000000000', 10) <
            parseInt('10000000000000001', 10)
    );
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/yociz/1/edit)

Q. What's the result?

```
(function() {
    return (0.1).toFixed(20);
})();
```

A.

```javascript
"0.10000000000000000555"
```

[JSBin](http://jsbin.com/vewuge/1/edit)

Q. What's the result?

```
(function() {
    return 1 / '';
})();
```

A.

```javascript
Infinity
```

[JSBin](http://jsbin.com/fepidu/1/edit)

Q. What's the result?

```
(function() {
    return 0 / '';
})();
```

A.

```javascript
NaN
```

[JSBin](http://jsbin.com/jemeki/1/edit)

Q. What's the result?

```
(function() {
    return 1 * null;
})();
```

A.

```javascript
0
```

[JSBin](http://jsbin.com/xocol/1/edit)

Q. What's the result?

```
(function() {
    return new Array() == false;
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/mexanu/1/edit)

# License

Released under the MIT License.
