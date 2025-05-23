# Dotchain 白皮書

# Dotchain
Dotchain 是一種函數式編程語言. 文件後綴`.dc`，命名為dot chain是因為我希望這個語言風格主要以`.`鏈式調用為主。啓發自`Elixir`的管道符號`|>`，如果直接使用`.`作為管道符是不是更方便。

# 願景
我希望Dotchain能實現我幾個想法，第一它將會是一種函數式編程語言，第二它將原生支持基於Actor model的並發編程模型，第三它將是運行在一個特殊的運行時上，一個類似於JVM 和 Erlang BEAM VM 的運行時上。

# 運行時 (Dotchain VM)
Dotchain VM將會是一個特別的運行時，一個雲原生的運行時，它將原生支持FaaS。它會是一個厚重的運行時，可以直接作為容器被cgroups和k8s運行。甚至能作為虛擬機直接啓動於QEMU中。我認為運行時將越來越厚重，直接在運行時上實現container cri，可直接被k8s等技術管理。

# 特性
1. 函数式編程
2. 模式匹配
3. 鏈式調用
4. Actor 並發模型
5. 靜態強類型
6. 柯里化

# Dotchain VM
Dotchain VM 是雲原生面向多租戶的虛擬機，因此沒有本地IO，一切都透過Actor和message來進行溝通。廠商應該提供與Actor溝通的方法和實現。
該虛擬機實現了兩個特殊的指令，`send`和`receive`用於發送和接收message。
## 指令
```
IPUSH 5      ; 放5至棧頂
FPUSH 5
IADD        ; pops two values on top of the stack, adds them pushes to stack
FADD
ISUB
FSUB
IMUL
FMUL
IDIV
FDIV
POP         ; pops the value on the stack, will also print it for debugging
SET 5 0     ; 把本地變量索引為5的值設為0
HLT         ; stop the program
```
