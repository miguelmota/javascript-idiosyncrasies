# JavaScript Idiosyncrasies (kinda)

This is a growing collection of some JavaScript idiosyncrasies, and a few things that might not be well recognized so I want to make aware.

If you can explain *why* the answer is to all questions then you are truly a JavaScript ninja. Some of these are just to confuse the reader, and by no means encourage best practices and should never be seen in production code. It's simply to demonstrate the *good* and *bad* parts of JavaScript.

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

[JSBin](http://jsbin.com/xogaki/1/edit) | [JSBin explained](http://jsbin.com/kadoko/1/edit)

Q. What's the result?

```javascript
function f() {
    return 'foo';
}
(function() {
    if (1 === 0) {
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

[JSBin](http://jsbin.com/lotavo/1/edit) | [JSBin explained](http://jsbin.com/xezad/1/edit)

Q. What's the result?

```javascript
(function() {
    return NaN === NaN;
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/katana/2/edit) | [JSBin explained](http://jsbin.com/xorix/1/edit)

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

[JSBin](http://jsbin.com/yutuce/1/edit) | [JSBin explained](http://jsbin.com/qemuf/1/edit)

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

[JSBin](http://jsbin.com/focobo/1/edit) | [JSBin explained](http://jsbin.com/lopoh/1/edit)

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

[JSBin](http://jsbin.com/hajus/1/edit) | [JSBin explained](http://jsbin.com/yulahi/1/edit)

Q. What's the result?

```javascript
(function(a, b, c) {
  delete arguments[0];

  return arguments.length;
})(1, 2, 3);
```

A.

```javascript
3
```

[JSBin](http://jsbin.com/gicij/1/edit) | [JSBin explained](http://jsbin.com/xobap/1/edit)

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

[JSBin](http://jsbin.com/rusas/1/edit) | [JSBin explained](http://jsbin.com/cofam/1/edit)

Q. What's the result?

```javascript
(function(a, b) {
   var foo, bar;

   foo = (bar = a, b);

   return foo;
})(1, 2);
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/dahaw/1/edit) | [JSBin explained](http://jsbin.com/heteg/1/edit)

Q. What's the result?

```javascript
(function(undefined) {
  var foo;
  return foo === undefined;
})(true);
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/vurego/1/edit) | [JSBin](http://jsbin.com/qabuye/1/edit)

Q. What's the result?

```javascript
(function(n) {
    return ~(n);
})(-3);
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/begehe/1/edit) | [JSBin explained](http://jsbin.com/buzabo/1/edit)

Q. What's the result?

```javascript
(function(n) {
    return ~~n;
})(-1.5);
```

A.

```javascript
-1
```

[JSBin](http://jsbin.com/roniwu/2/edit) | [JSBin explained](http://jsbin.com/kijuze/1/edit)

Q. What's the result?

```javascript
(function(x) {
    return !!x;
})('a');
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/rahuy/1/edit) | [JSBin explained](http://jsbin.com/yegix/1/edit)

Q. What's the result?

```javascript
(function() {
    return typeof null === 'null';
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/nurihe/5/edit) | [JSBin explained](http://jsbin.com/yeroke/1/edit)

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

[JSBin](http://jsbin.com/lobib/2/edit) | [JSBin explained](http://jsbin.com/viwoba/1/edit)

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

[JSBin](http://jsbin.com/loxim/1/edit) | [JSBin explained](http://jsbin.com/cigis/1/edit)

Q. What's the result?

```javascript
(function() {
    return ''+(new Date());
})();
```

A.

```javascript
"Sun Mar 02 2014 18:14:01 GMT-0800 (PST)"
```

[JSBin](http://jsbin.com/hiheq/2/edit) | [JSBin explained](http://jsbin.com/yirey/1/edit)

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

[JSBin](http://jsbin.com/mifiy/1/edit) | [JSBin explained](http://jsbin.com/pegavu/1/edit)

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

[JSBin](http://jsbin.com/foqoc/1/edit) | [JSBin explained](http://jsbin.com/sojow/1/edit)

Q. What's the result?

```javascript
(function() {
    return (function(){}) === (function(){});
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/yikero/2/edit) | [JSBin explained](http://jsbin.com/cuzub/1/edit)

Q. What's the result?

```javascript
(function(n) {
    return n === new Number(n);
})(10);
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/jivini/1/edit) | [JSBin explained](http://jsbin.com/titemi/1/edit)

Q. What's the result?

```javascript
(function(x) {
    return new String(x) === x;
})('a');
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/femeto/1/edit) | [JSBin explained](http://jsbin.com/xelado/1/edit)

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

[JSbin](http://jsbin.com/nilagi/1/edit) | [JSBin explained](http://jsbin.com/nezow/1/edit)

Q. What's the result?

```javascript
(function() {
    var obj1 = { foo: 'bar' },
        obj2 = { foo: 'bar' };

    return obj1 === obj2;
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/dokej/1/edit)| [JSBin explained](http://jsbin.com/kocoma/1/edit)

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

[JSBin](http://jsbin.com/culufi/1/edit) | [JSBin explained](http://jsbin.com/zuyuv/1/edit)

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

    return o + o;
})();
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/qinol/1/edit) | [JSBin explained](http://jsbin.com/wizemo/1/edit)

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

[JSBin](http://jsbin.com/pibob/1/edit) | [JSBin explained](http://jsbin.com/lusuc/1/edit)

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

[JSBin](http://jsbin.com/cawiro/1/edit) | [JSBin explained](http://jsbin.com/tacet/1/edit)

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

[JSBin](http://jsbin.com/kucob/1/edit) | [JSBin explained](http://jsbin.com/sidija/1/edit)

Q. What's the result?

```javascript
(function() {
    var x = 1;

    return (function () {
        return x;

        var x = 2;
    })();
})();
```

A.

```javascript
undefined
```

[JSBin](http://jsbin.com/kesori/1/edit) | [JSBin explained](http://jsbin.com/zabat/1/edit)

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

[JSBin](http://jsbin.com/mopab/1/edit) | [JSBin explained](http://jsbin.com/sisari/2/edit)

Q. What's the result?

```javascript
(function() {
    var n;

    function name() {
        return this.name
    };

    n = name.bind({name: 'foo'});
    n = n.bind({name: 'bar'})

    return n();
})();
```

A.

```javascript
"foo"
```

[JSBin](http://jsbin.com/yokaw/1/edit) | [JSBin explained](http://jsbin.com/biruk/1/edit)

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

[JSBin](http://jsbin.com/xocol/1/edit) | [JSBin explained](http://jsbin.com/kuhec/1/edit)

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

[JSBin](http://jsbin.com/mexanu/1/edit) | [JSBin explained](http://jsbin.com/tizagi/2/edit)

# License

Released under the MIT License.
