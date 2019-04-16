### shell
  1. 使用环境变量
  ```shell
  `date` || $(date)
  ```
  `./t.sh & //&代表后台运行` 
  2. 执行运算
  ```shell
    a=10
    b=20 # 不能又空格
    c=$(expr $a + $b) # 变量必须用空格隔开

    # 也可以这么运算
    c=$[$a + $b]
  ``` 
  3. bc
  ```shell
    $(bc << EOF
    scale = 4
    a1 = ( $var1 * $var2)
    b1 = ($var3 * $var4)
    a1 + b1
    EOF
    )
  ```
  4. 退出
  ```shell
  exit 11 0代表成功
  echo $?
  ```
#### 结构化命令
  1. if-then if-then-elif-then-fi   if-test-condtion
  2. 数值比较
   - n1 -eq n2 检查n1是否与n2相等
   - n1 -ge n2 检查n1是否大于或等于n2
   - n1 -gt n2 检查n1是否大于n2
   - n1 -le n2 检查n1是否小于或等于n2
   - n1 -lt n2 检查n1是否小于n2
   -  n1 -ne n2 检查n1是否不等于n2
  3. 字符串比较
   - str1 = str2 检查str1是否和str2相同 
   - str1 != str2 检查str1是否和str2不同 
   - str1 < str2 检查str1是否比str2小 \< 需要转译 
   - str1 > str2 检查str1是否比str2大 \> 需要转译 
   - -n str1 检查str1的长度是否非0 
   - -z str1 检查str1的长度是否为0
  4. 文件比较
   - -d file 检查file是否存在并是一个目录
   - -e file 检查file是否存在 
   - -f file 检查file是否存在并是一个文件
   - -r file 检查file是否存在并可读 
   - -s file 检查file是否存在并非空
   - -w file 检查file是否存在并可写
   - -x file 检查file是否存在并可执行
   - -O file 检查file是否存在并属当前用户所有
   - -G file 检查file是否存在并且默认组与当前用户相同
   - file1 -nt file2 检查file1是否比file2新
   - file1 -ot file2 检查file1是否比file2旧
  5. 复合条件
   - && 
   - ||
  6. if-then 高级
   - ((双括号)) 可以进行高级运算 ++ -- ! ~ ** || | &
   - [[]] 不是所有的shell 都支持 可以进行模式匹配
   - case in rich) esac
  7. for
  ```bash
  for var in a v this't' #单引号会被去掉 可以用双引号包起来or \转译 
  do
    echo $var
  done
  file="states" # 变量读取值
    for state in $(cat $file)
    do
        echo "Visit beautiful $state"
    done
  for ((i = 0;i < 10; i ++))
  do
    echo $i
  done
  ```
  8. while
  ```bash
  i=0
  while [ $i -lt 10 ]
  do
    if [ $i -eq 4 ]
    then
     continue 
    fi
    echo $i
    if [ $i -eq 5 ]
    then
      break
    fi
    i=$[ $i + 1 ]
  done
  ```
#### 命令行参数
  1. $i 第i个参数 $0 文件名 $# 参数个数
  2. 获取用户输入
  ```bash
  #!/bin/bash
  # testing the read command
  #
  echo -n "Enter your name: "
  read name -t 5 #超时时间
  echo "Hello $name, welcome to my program. "
  exec # 永久重定向
  ```
  3. nice 指定命令优先级 -n 10 renice 更改运行中优先级 
  4. function 指定函数
  ```bash
    #声明函数
    function f{
      echo '1212'
      lll # 执行错误函数
      return 111 # return 值
      echo '12' # 输出的返回值 需要$ 去接受
    }
    #调用函数
    f
    echo $? # 函数错误状态码
  ```
  - 添加参数
  ```bash
    # 声明函数 
    function f{
      echo $1
      echo $2
    }
    # 执行函数 传递参数
    f 1 2
    # 执行
    ./t.sh
    #结果
    1
    2

    #变量赋值
    value=10 # 全局变量
    function f {
      read -p "please input value:::  " value
    }
    function f1 {
      read -p "please input value::" local value
    }
    f
    f1 # 外部读取不到local定义的变量
    echo $value
  ```
  - 传递数组参数
  ```bash
        echo "The parameters are : $@"

        #函数只会读取数组变量的第一个值
        thisarray=$1
        echo "The received array is ${thisarray[*]}"

        local newarray
        newarray=(`echo "$@"`) # 数据必须新建数组去接受
        echo "The new array value is : ${newarray[*]}"
        myarray=(1 2 3 4 5)
        echo "The original array is : ${myarray[*]}"

        #将数组变量当成一个函数参数，函数只会去函数变量第一个值
        #testit $myarray
        # 传递所有数组参数
        testit ${myarray[*]}
        # 返回数组
        echo ${newarray[*]}
  ```
  - 接受外部参数递归
  ```bash
  function f {
  if [ $1 -eq 1 ]
   then
     echo 1
   else
    local temp=$[ $1 - 1 ]
    local result=$(f $temp)
    echo $[ $1 * $result ]
   fi
  }
  f $1
  ```
  - 引入外部库
  ```bash
  . ./bash #引用外部库
  f # 调用外部库函数
  ```