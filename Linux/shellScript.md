## Shell Script
#### 1 什么是Shell Script
    注意：
    1、指令的执行是从上到下、从左到右执行的
    2、指令与参数之间的多个空白都会忽略
    3、空白行也将被忽略
    4、Enter执行
    5、如果一行内容太多可以【\[Enter]】进行换行
    6、【#】注释
    执行文档(/home/dmtsai/shell.sh)：
    1、直接下达：shell.sh文档必须要具备可读可执行（rx）的权限，然后：
        绝对地址：使用/home/dmtsai/shell.sh
        相对路径：假设工作目录在/home/dmtsai/, 则使用./shell.sh来执行
        [path]功能：将shell.sh放到PATH指定的目录内，例如./bin/
    2、以bash方式来执行：通过bash shell.sh或sh shell.sh来执行
    
##### 1.2 第一个shell script
    下载vim sudo apt-get install vim

#### 2 简单的shell script练习
##### 2.1.1 输入输出工具
    echo "输出内容"   
    read -p "提示内容" 变量
##### 2.1.2 数据类型
    shell 赋值默认为字符串，所以在进行计算时应注意：
    $((运算内容))  整数
    echo "123.123*55.9" | bc   计算小数时
##### 2.1.3 shell运行方式
    base
    sh shell脚本文件中 
    bash shell脚本文件
    
##### 2.1.4 script的执行方式差异
    sh 运行脚本在子程序中
    source 运行脚本在父元素中
#### 3 判断语句
##### 3.1 利用test指令测试功能
    test指令结合$?($?变量指上层代码的错误代码) &&与 ||或
    test -e /aa && echo "有aa" || echo "没有aa"
    
##### 3.2 利用判断号[]
    [ -f "sourefile" ] 判断是否为一个文件
    [ -d "directory" ] 判断是否为一个路径
    [ -x "bin/ls" ] 判断是否为一个可执行文件
    [ -n "$var" ] 判断$var是否有值
    [ "$a" == "$b" ] 判断$a是否等于$b
##### 3.2.1 算术运算符
    +
    -
    *
    /
    %
##### 3.2.1 赋值运算符
    =
##### 3.2.1 关系运算符
    -eq 相等
    -ne 不相等
    -gt 大于
    -lt 小于
    -ge 大于等于
    -le 小于等于
    ==
    !=
    >
    <
    >=
    <=
##### 逻辑运算符
    ! 非
    -o 或
    -a 与
    ||
    &&
##### 字符串运算符
    =   
    !=
    -z 检测字符串为0  为0返回true
    -n 检测字符串为0  不为0返回true
    str 检测字符串是否为空 不为空返回true
##### 文件测试运算符
    -d 是否为目录
    -f 是否为文件
    -x 是否可执行
    -r 是否可读
    -w 是否可写
    -s 是否为空
    -e 是否存在
    
##### 3.3 shellscript 预设变数
    变量名=值  等于号两端不加空格
    $变量名
    ${变量名}
#### 4 条件判断语句
##### 4.1 if then
    if 判断条件; then
    elif 判断条件; then
    else
    fi
    # 判断文件还是路径的脚本
    if [ -f a.sh ] then;
        echo "这是文件"
    else
        echo "这是路径"
    fi   
##### 4.2 利用case ease
    语法：
    case $变数名称 in
        "第一个变数内容")
            程序
            ;;
        "第二个变数内容")
            程序
            ;;
        *)
            程序最后
            ;;
    esac   
    
    判断输入内容
    case ${1} in
      "hello")
        echo "Hello, how are you ?"
        ;;
      "")
        echo "You MUST input parameters, ex> {${0} someword}"
        ;;
      *)    #其实就相当于万用字元，0~无穷多个任意字元之意！
        echo "Usage ${0} {hello}"
        ;;
    esac
##### 4.3 利用function功能
    function 函数名(){
        程序
    }
    函数名 直接调用
    没有形式参数
#### 5 循环
##### 5.1 while do done ,until do done
    语法：
    while 判断式
    do
        程序
    done
        程序
    举例：
    s=0
    i=0
    while [ "${i}"!="100"]
    do
        i=$(($i+1))
        s=$(($s+$i))
    done
        echo "$s"
    
##### 5.2 for do done
    语法：
        for var in con1 con2 con3
        do
            程序
        done
            程序
      
##### 5.3 for do done的数值处理
    for ((初始值;条件;步进值))
    do
        程序
    done
    
    bash 执行
##### 5.4 数组
    数组创建：
    1、
    arr[1]=aa
    arr[2]=bb
    ……
    2、
    arr=(aa bb cc dd)
    数组的长度
    ${#arr[@]}  
    数组的访问
    ${arr[index]} 访问元素
    ${arr[@]}  访问数组 
    数组的遍历
    for i in ${arr[@]}
    do
        echo $i
    done
        echo "over"
    切片:
    ${arr[@]:0:3}