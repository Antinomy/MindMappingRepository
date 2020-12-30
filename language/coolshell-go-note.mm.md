# GO编程模式
## 切片，接口，时间和性能
### 切片 Slice
#### 不是数组，而是一个结构体
#### 内存共享
#### append() 可能导致重新分配内存
### 深度比较
#### 使用反射 reflect.DeepEqual(a,b)
### 接口编程
#### 是一种抽象，主要是用在“多态”
#### 面向对象编程的黄金法则——“Program to an interface not an implementation”
#### 接口完整性检查
##### 标准的作法 var _ Shape = (*Square)(nil)
###### 声明一个 _ 变量（没人用），其会把一个 nil 的空指针，从 Square 转成 Shape，如果没有实现完相关的接口方法，编译器就会报错
### 时间
#### 重用已有的时间处理
##### time.Time
##### time.Duration
#### 全球化跨时区的应用，把所有服务器和时间全部使用UTC时间。
### 性能提示
#### 数字转字符串，使用 strconv.Itoa() 会比 fmt.Sprintf() 要快一倍左右
#### String转成[]Byte会导致性能下降
#### 如果在for-loop里对某个slice 使用 append(),请先把 slice的容量很扩充到位,避免内存重新分享浪费内存
#### 用StringBuffer / StringBuild 拼接字符串，会比使用 + 或 += 性能高三到四个数量级
#### 尽可能的使用并发的 go routine，然后使用 sync.WaitGroup 来同步分片操作
#### 避免在热代码中进行内存分配，这样会导致gc很忙。尽可能的使用 sync.Pool 来重用对象。
#### 使用 lock-free的操作，避免使用 mutex，尽可能使用 sync/Atomic包
#### 使用 I/O缓冲，I/O是个非常非常慢的操作，使用 bufio.NewWrite() 和 bufio.NewReader() 可以带来更高的性能。
#### 对于在for-loop里的固定的正则表达式，一定要使用 regexp.Compile() 编译正则表达式。性能会得升两个数量级。
#### 如果你需要更高性能的协议，你要考虑使用 protobuf 或 msgp 而不是JSON，因为JSON的序列化和反序列化里使用了反射。
#### 你在使用map的时候，使用整型的key会比字符串的要快，因为整型比较比字符串比较要快。
