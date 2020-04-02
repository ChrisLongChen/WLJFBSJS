# checkUDP.py
```
from matplotlib import pyplot as plt
import numpy as np

def Oxtrans(n):
    n1 = bin(n)
    num = n1[2:]
    if len(num) < 16:
        number = '0' + num
    return num

def add(num1, num2):
    result = num1 + num2
    maxNum = (2 ** 16) - 1
    while result > maxNum:  #溢出回卷
        result = result - maxNum
    return result

def FindUDP(num):
    if num[0] == '0':
        udp = '1'
    elif num[1] == '1':
        udp = '0'
    for i in range(1, 16):
        if num[i] == '0':
            udp = udp + '1'
        elif num[i] == '1':
            udp = udp + '0'
    return udp

def testUDP(udp, result):
    # 把输入的三个数字和检验和相加
    Tresult = udp + result
    Tresult = Oxtrans(Tresult)
    Tlist = []
    for num in Tresult:
        Tlist.append(num)
    x = np.arange(1, 17)
    plt.title('UDP test')
    plt.plot(x, Tlist, "ob")
    plt.show()

if __name__ == '__main__':
    num1 = input('Please input the first number:')
    num2 = input('Please input the second number:')
    num3 = input('Please input the third number:')
    #十进制转换
    num1 = int(num1, 2)
    num2 = int(num2, 2)
    num3 = int(num3, 2)

    result1 = add(num1, num2)
    result2 = add(result1, num3)
    result = Oxtrans(result2)
    print('The result is:', result)
    udp = FindUDP(result)
    print('The checksum is', udp)
    int_udp = int(udp, 2)
    testUDP(int_udp, result2)
```
