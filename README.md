<h3 align="center">
  <br />
  <img src="https://user-images.githubusercontent.com/168240/51433988-e04f7600-1c0c-11e9-9b06-217d668dcc79.png" alt="logo" width="700" />
  <br />
  <br />
  <br />
</h3>

# JavaScript idiosyncrasies

> This is a collection of things in JavaScript that may not be well recognized, espcially to beginners.

[![License](http://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/miguelmota/javascript-idiosyncrasies/master/LICENSE)

Disclaimer: Some of these snippets are simply to demonstrate the *quirky* parts of JavaScript and by no means encourage best practices and should never be seen in production code.

---

In no particular order:

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

[JSBin](http://jsbin.com/focobo/1/edit) | [JSBin explained](http://jsbin.com/lopoh/2/edit)

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
    return {foo: 'bar'} === {foo: 'bar'};
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
    for(;;);
    return 1;
})();
```

A.

```javascript
*Infinite loop*
```

[JSBin](http://jsbin.com/rerati/1/edit) | [JSBin explained](http://jsbin.com/dukagu/1/edit)

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

[JSBin](http://jsbin.com/pufaqiwuri/1/edit) | [JSBin explained](http://jsbin.com/zabat/1/edit)

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

[JSBin](http://jsbin.com/mohuf/1/edit) | [JSBin explained](http://jsbin.com/pileko/1/edit)

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

[JSBin](http://jsbin.com/warowo/1/edit) | [JSBin explained](http://jsbin.com/sudut/1/edit)

Q. What's the result?

```javascript
(function() {
    return Math.pow(2,1024) === Infinity;
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/xozim/1/edit) | [JSBin explained](http://jsbin.com/vohoco/1/edit)

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

[JSBin](http://jsbin.com/dijiqo/1/edit) | [JSBin explained](http://jsbin.com/wefaw/1/edit)

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

[JSBin](http://jsbin.com/nedupi/1/edit) | [JSBin explained](http://jsbin.com/fuwuz/1/edit)

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

[JSBin](http://jsbin.com/vewuge/1/edit) | [JSBin explained](http://jsbin.com/lupaxi/1/edit)

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

[JSBin](http://jsbin.com/wuxobi/1/edit) | [JSBin explained](http://jsbin.com/letef/1/edit)

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

[JSBin](http://jsbin.com/sugewu/1/edit) | [JSBin explained](http://jsbin.com/disuzo/1/edit)

Q. What's the result?

```
(function() {
    return (parseInt('10000000000000000', 10) ===
            parseInt('10000000000000001', 10)
    );
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/yociz/1/edit) | [JSBin explained](http://jsbin.com/jefera/1/edit)

Q. What's the result?

```javascript
(function(n) {
    return (Function)('var n = n || 2; return n;')(n);
})(1);
```

A.

```javascript
2
```

[JSBin](http://jsbin.com/tujig/1/edit) | [JSBin explained](http://jsbin.com/redup/2/edit)

Q. What's the result? (assuming window scope)

```javascript
var a = 1;
b = 1;

(function() {
  return (delete window.a) === (delete window.b);
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/cowoji/1/edit) | [JSBin explained](http://jsbin.com/ceriwu/1/edit)

```javascript
(function(x) {
  var isMatch,
      regex = /[\w]/gi;

  return (regex.test(x) === regex.test(x));
})('a');
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/kulavu/2/edit) | [JSBin explained](http://jsbin.com/hamog/1/edit)

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

[JSBin](http://jsbin.com/puyap/1/edit) | [JSBin explained](http://jsbin.com/mavicu/1/edit)

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

[JSBin](http://jsbin.com/huboca/1/edit) | [JSBin explained](http://jsbin.com/xudanu/1/edit)

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

[JSBin](http://jsbin.com/vetiba/1/edit) | [JSBin explained](http://jsbin.com/dipedereti/edit)

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

[JSBin](http://jsbin.com/dulih/1/edit) | [JSBin explained](http://jsbin.com/veruri/1/edit)

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

[JSBin](http://jsbin.com/lekun/1/edit) | [JSBin explained](http://jsbin.com/xukis/1/edit)

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

[JSBin](http://jsbin.com/femicu/1/edit) | [JSBin explained](http://jsbin.com/cotaf/1/edit)

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

[JSBin](http://jsbin.com/fepidu/1/edit) | [JSBin explained](http://jsbin.com/hofutu/1/edit)

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

[JSBin](http://jsbin.com/mexanu/1/edit) | [JSBin explained](http://jsbin.com/tizagi/3/edit)

Q. What's the result?

```javascript
(function() {
  if ([]) {
    return [] == false;
  }
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/cuyer/1/edit) | [JSBin explained](http://jsbin.com/suzev/1/edit)

Q. What's the result?

```javascript
(function() {
  return ''.concat(null);
})();
```

A.

```javascript
"null"
```

[JSBin](http://jsbin.com/mobaqepetu/1/edit) | [JSBin explained](http://jsbin.com/xiwakihaxa/1/edit)

Q. What's the result?

```javascript
(function(a, b) {
  return a + + b;
})('a','b');
```

A.

```javascript
"aNaN"
```

[JSBin](http://jsbin.com/wenifelaco/1/edit) | [JSBin explained](http://jsbin.com/bivuzupaje/1/edit)

Q. What's the result?

```javascript
(function() {
  Object.prototype.foo = 'foo';

  return foo;
})();
```

A.

```javascript
"foo"
```

[JSBin](http://jsbin.com/jogeroluru/1/edit) | [JSBin explained](http://jsbin.com/wajumigoru/1/edit)

Q. What's the result?

```javascript
(function() {
  return 1000 === 1e3;
})();
```

A.

```javascript
true
```

[JSBin](http://jsbin.com/xafixizapo/1/edit) | [JSBin explained](http://jsbin.com/zigozeheti/1/edit)

Q. What's the result?

```javascript
(function() {
  return 9999999999999999;
})();
```

A.

```javascript
10000000000000000
```

[JSBin](http://jsbin.com/detarakare/1/edit) | [JSBin explained](http://jsbin.com/bisinayicu/1/edit)

Q. What's the result?

```javascript
(function() {
  (function() {
    var a = b = 1;
  })();

  return typeof a === typeof b;
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/rudokoqiza/1/edit) | [JSBin explained](http://jsbin.com/qubokakuga/1/edit)

Q. What's the result?

```javascript
(function() {
  return Array(3).map(function(o) { return 'a'; });
})();
```

A.

```javascript
[undefined, undefined, undefined]
```

[JSBin](http://jsbin.com/nafuhuyeka/1/edit?html,js,console) | [JSBin explained](http://jsbin.com/pamafoxuto/1/edit)

Q. What's the result?

```javascript
(function() {
  var foo = [0,1,2];
  foo[10] = 10;
  return foo.filter(function(n) { return n === undefined; });
})();
```

A.

```javascript
[]
```

[JSBin](http://jsbin.com/taqewiside/1/edit) | [JSBin explained](http://jsbin.com/sokatasosu/1/edit)

Q. What's the result?

```javascript
(function(x) {
  var ret = null;

  switch(x) {
    case 'A':
        ret = 'A';
        break;
    default:
        ret = 'unknown';
        break;
  }

  return ret;
})(new String('A'));
```

A.

```javascript
"unknown"
```

[JSBin](http://jsbin.com/zawezozepe/1/edit) | [JSBin explained](http://jsbin.com/leyaqamuru/1/edit?html,js,consol:w
jke)

Q. What's the result?

```javascript
(function() {
  var x = {};

  return x.prototype === Object.getPrototypeOf(x);
})();
```

A.

```javascript
false
```

[JSBin](http://jsbin.com/fokomolova/1/edit) | [JSBin explained](http://jsbin.com/coxakaxiwu/1/edit?html,js,console)

Q. What's the result?

```javascript
(function() {
  function foo() {}
  foo.name = 'bar';

  return foo.name;
})();
```

A.

```javascript
"foo"
```

[JSBin](http://jsbin.com/bequxifegi/1/edit) | [JSBin explained](http://jsbin.com/zenipunohi/1/edit)

Q. What's the result?

```javascript
(function() {
  return Array(5).join(',').length;
})();
```

A.

```javascript
4
```

[JSBin](http://jsbin.com/cabalutozu/1/edit) | [JSBin explained](http://jsbin.com/yewopuxohi/1/edit)


Q. What's the result?

```javascript
(function(x) {
  return x++ + ++x;
})(2);
```

A.

```javascript
6
```

[JSBin](https://jsbin.com/laqebotenu/edit?js,console) | [JSBin explained](https://jsbin.com/tukutofimi/edit?js,console)


Q. What's the result?

```javascript
(function() {
  'use strict';

  let type = typeof foo;
  let foo = 1;

  return type;
})();
```

A.

```javascript
ReferenceError: foo is not defined
```

---

## License

[MIT](LICENSE)
