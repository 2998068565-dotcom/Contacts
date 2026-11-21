# 通讯录（Contacts）

C 语言课程练习：**动态数组**实现的通讯录，数据以二进制形式保存在同目录的 `Contact.txt`。

## 文件

| 文件 | 作用 |
| --- | --- |
| `Contact.h` | 结构体 `PeoInfo`/`Contact` 定义与函数声明 |
| `Contact.c` | 全部功能实现：菜单、加载/保存、增删改查、排序、增容 |
| `test.c` | 入口 `main`：菜单循环，退出时保存并释放内存 |

## 功能

1. 添加联系人
2. 删除联系人（按姓名查找后前移覆盖）
3. 查找联系人
4. 修改联系人
5. 显示全部联系人
6. 按姓名排序（`qsort`）
0. 退出（保存到 `Contact.txt` 并释放内存）

## 数据结构

```c
typedef struct PeoInfo {
    char name[20];
    int  age;
    char sex[10];
    char tele[12];
    char addr[30];
} PeoInfo;

typedef struct Contact {
    PeoInfo* data;   // 动态数组
    int count;       // 当前数量
    int capacity;    // 当前容量
} Contact;
```

- 初始容量 `INI_DATA = 3`，每次扩容 `INC_SZ = 2`。
- 启动时 `LoadContact` 从 `Contact.txt` 读入，退出时 `SaveContact` 写回。
- 文件用 `fread`/`fwrite` 直接读写结构体，属于二进制格式。

## 编译运行

```bat
cl Contact.c test.c
test.exe
```

头文件里已定义 `_CRT_SECURE_NO_WARNINGS`，MSVC 编译无需额外参数。

源码是 **GBK（代码页 936）** 编码；用 gcc/MinGW 建议加 `-fexec-charset=GBK` 或先转 UTF-8。

## 说明

- 课程练习代码，保留了注释和被注释掉的旧实现（如静态数组版 `InitContact`、`AddContact`）。
- `Contact.txt` 是运行后生成的二进制数据文件，不纳入版本库。
- 二进制格式依赖结构体内存布局，换编译器或改结构体后旧文件可能读不出来。
