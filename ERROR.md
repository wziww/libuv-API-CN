# 错误处理(Error handling)

在libuv中 错误(errors)是以常量形式形式出现的,根据经验，当出现一个状态参数，或者API函数返回了一个整数，这个常量表示了一个错误(error)。

当一个函数返回了一个错误，这个函数的回调函数永远不会被调用。

```js
console.log('My first method');
```


## 错误常量

#### UV_E2BIG (-7)

{% sample lang="js" %}
参数列表过长

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
