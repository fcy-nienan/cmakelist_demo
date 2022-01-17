cmake_minimum_required(VERSION 3.19)
project(cmakelist_demo)

set(CMAKE_CXX_STANDARD 14)
# 设置变量
set(fcy 123)
message(" var = ${fcy}")# var = 123
message("PATH = $ENV{PATH}")# path = xxxxxxx

set(inner_var foo)
set(outer_foo_var 999)
message("nest variable value is :${outer_${inner_var}_var}")#nest variable value is :999

# set(列表名 值1 值2 ... 值N)
# 或者
# set(列表名 “值1;值2; ...;值N”)
set(list_var 1 2 3 4)
set(list_foo "5;6;7;8")
message(${list_var})#1234
message(${list_foo})#5678
message("${list_var}")#1;2;3;4
message("${list_foo}")#5;6;7;8

# 流程控制
#一元	EXISTS, COMMAND, DEFINED.
#二元	EQUAL, LESS, LESS_EQUAL, GREATER, GREATER_EQUAL, STREQUAL,STRLESS, STRLESS_EQUAL, STRGREATER, STRGREATER_EQUAL,VERSION_EQUAL, VERSION_LESS, VERSION_LESS_EQUAL, VERSION_GREATER, VERSION_GREATER_EQUAL,MATCHES
#逻辑	NOT, AND, OR
#true	1, ON, YES, TRUE, Y, 非0的值
#false	0, OFF, NO, FALSE, N, IGNORE, NOTFOUND, 空字符串””, 以-NOTFOUND 结尾的字符串
set(if_1_con 1)
set(else_1_con 1)
if(${if_1_con})
    message("if branch")
elseif(${else_1_con})
    message("elseif branch")
else()
    message("else branch")
endif()

#循环
set(a "")

while(NOT a STREQUAL "xxxxx")
    set(a "${a}x")
    message("  a = ${a}")
endwhile()

foreach(item "A" "B" "C")
    message("  ${item}")
endforeach(item)

foreach(x RANGE 10 14 2)
    message("  ${x}")
endforeach(x)

set(list_var "1;2;3;4")
foreach(x IN LISTS list_var)
    message("  ${x}")
endforeach(x)

set(x 3)
foreach(i RANGE 1 4 1)
    message(${i})
    if(${i} LESS ${x})
        break()
    else()
        continue()
    endif()
endforeach(x)


# 函数
function(foo x y z)
    message("Calling function 'foo':")
    message("  x = ${x}")
    message("  y = ${y}")
    message("  z = ${z}")
    message("ARGC = ${ARGC} arg1 = ${ARGV0} arg2 = ${ARGV1} arg3 = ${ARGV2} all args = ${ARGV}")
endfunction(foo)

foo("1" "2" "3")


add_executable(cmakelist_demo main.cpp)
