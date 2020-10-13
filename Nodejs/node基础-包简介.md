### 包package

包实际上就是一个压缩文件，解压以后还 原为目录。符合规范的目录，应该包含如下文件：

– package.json 		描述文件(相当于说明书)-------唯一一个必须有的

 – bin 						可执行二进制文件

 – lib						   js代码 

– doc 						文档 

– test 						单元测试

### package.json

# 注意：任何JSON文件都不能写注释

package.json中的字段：

 name、description、version、keywords、 maintainers、contributors、bugs、 licenses、repositories、dependencies、 homepage、os、cpu、engine、builtin、 directories、implements、scripts、author、 bin、main、devDependencies......

###### dependencies：依赖

###### description：描述

###### devDependencies：开发依赖