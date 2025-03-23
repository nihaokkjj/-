.cout:
输出格式为：

①定义：double name = 0;

②输出：cout << fixed << setprecision（2） << name <<endl;

在这里解释一下fixed和setprecision：

fixed是一个操纵器，用于指定浮点数的输出格式为固定小数点形式

结合fixed时，setprecision只影响小数点后的位数。

没有fixed时，setprecision控制有效数字的总个数（即包括小数点前后的所有数字）。他会用科学计数法来表示超出有效数字的部分

例如：

cout << setprecision(2) << double <<endl;

输入：333.33

输出3.3e+002
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
                        
原文链接：https://blog.csdn.net/ndjdjjsdhjdj/article/details/143648695