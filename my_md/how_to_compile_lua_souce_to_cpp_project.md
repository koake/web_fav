### ref https://blog.csdn.net/pangjiuzala/article/details/52587976
# 如何编译lua源码到cpp项目中引用  Windows part
-----
### 准备以下东西
- lua 源码，可以从lua官网下载
- VS开发环境，并且支持c++

### 步骤
- 新建一个工程，选择静态库的形式，或者在项目创建好之后再设置页中的 `配置属性->常规->配置类型` 中切换
- 分别导入包中src下的 .h 与 .c 文件
- 移除 `lua.c luac.c` 的引用
- 选择工程 `属性 -> C/C++ -> 高级 -> 编译为 -> C/TC （若没有此项创建一个cpp文件即可）`
- 选择工程，生成 (生成的路径与生成的名字与设置有关，在此不赘述）
- 完工




# 如何将编译好的lua静态库引用到cpp项目中 Windows part
-----
#### 准备以下东西
- 编译好的lua的lib
- 与编译好的lua对应的源码
- 新建一个cpp工程(默认命令行即可)
- 选择`项目 -> 链接器 -> 输入 -> 附加依赖性，将生产的lib加入其中`
- 选择`项目 -> C/C++ -> 常规 -> 附加包含目录 -> 将lua源码引入`
- 新建一个main.cpp与main.lua，例子如下
- 编译运行工程，会输出 Hello World Lua!!

```cpp
// main.cpp
#include<iostream>
#include<lua.hpp>

using namespace std;
int main() 
{
	lua_State *l = luaL_newstate();
	luaL_openlibs(l);
	luaL_dofile(l, "main.lua");
	lua_close(l);
	system("pause");
	return 0;
}
```


```lua
-- main.lua
local function hello()
	print("Hello World Lua!!")
end

hello()
```
