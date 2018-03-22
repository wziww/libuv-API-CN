# 错误处理(Error handling)

在libuv中 错误(errors)是以常量形式形式出现的,根据经验，当出现一个状态参数，或者API函数返回了一个整数，这个常量表示了一个错误(error)。

当一个函数返回了一个错误，这个函数的回调函数永远不会被调用。

```js
console.log('My first method');
```





{% method %}
## 错误常量

My first method exposes how to print a message in JavaScript and Go.

{% sample lang="js" %}
Here is how to print a message to `stdout` using JavaScript.

```js
console.log('My first method');
```

{% sample lang="go" %}
Here is how to print a message to `stdout` using Go.

```go
fmt.Println("My first method")
```

{% common %}
Whatever language you are using, the result will be the same.

```bash
$ My first method
```
{% endmethod %}
