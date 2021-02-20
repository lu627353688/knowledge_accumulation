注: lua 版本 5.1 

比较有用的方法:

格式化小数为百分比小数字符串(也允许带百分号)
```
local format_number = function(number, m, n)
    --[[
        number: 数字
        m: 保留之前乘的数字
        n: 保留的小数点位数
    ]]
    number = tostring(number)
    number, _ = string.gsub(number, "%%", "")
    number = tonumber(number)
    if number == nil or number == 0 then
        return 0
    end
    number = number * m
    local int, float = 0, 0
    local base = math.pow(10, n)
    int, float = math.modf(number * base)
    if float >= 0.5 then
        int = int + 1
    end
    return int / base
end

-- 比如:
print(format_number(0.11115, 1, 4)) -- 0.1112
print(format_number(0.11115, 100, 4)) -- 11.115
```