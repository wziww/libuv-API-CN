# Macros

### UV\_VERSION\_MAJOR

> libuv 主版本号

### UV\_VERSION\_MINOR

> libuv 次版本号

### UV\_VERSION\_PATCH

> libuv 版本修订号

### UV\_VERSION\_IS\_RELEASE

> 设置为 1 表示一个 libuv 版本, 0 为开发快照

### UV\_VERSION\_SUFFIX

> libuv 版本后缀, 某些开发版本可能有后缀, 例如 "rc"

### UV\_VERSION\_HEX

> 返回 libuv 版本打包成一个单一的整数。每个组件使用8位，补丁号存储在8个最小有效位中。例如libuv 1.2.3为0x010203.

```cpp
#ifndef UV_VERSION_H
#define UV_VERSION_H

 /*
 * Versions with the same major number are ABI stable. API is allowed to
 * evolve between minor releases, but only in a backwards compatible way.
 * Make sure you update the -soname directives in configure.ac
 * and uv.gyp whenever you bump UV_VERSION_MAJOR or UV_VERSION_MINOR (but
 * not UV_VERSION_PATCH.)
 */

#define UV_VERSION_MAJOR 1
#define UV_VERSION_MINOR 19
#define UV_VERSION_PATCH 3
#define UV_VERSION_IS_RELEASE 0
#define UV_VERSION_SUFFIX "dev"

#define UV_VERSION_HEX  ((UV_VERSION_MAJOR << 16) | \
                         (UV_VERSION_MINOR <<  8) | \
                         (UV_VERSION_PATCH))

#endif /* UV_VERSION_H */"dev"
```

_New in version 1.7.0._

# Functions

```cpp
unsigned int uv_version(void)
//Returns UV_VERSION_HEX.
```

```cpp
const char* uv_version_string(void)
//Returns the libuv version number as a string. For non-release versions the version suffix is included.
```



