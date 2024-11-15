# **Reverse Engineering**

## **Vault-Door-Series**

We are provided with a number of Java Programs that ask for password when executed. We have to find the password in each level. These passwords are infact the flags.

### **vault-door-training**

Compile the code `javac VaultDoorTraining.java` and execute the program by `java VaultDoorTraining`.
We are prompted to enter the password.`cat VaultDoorTraining.java` to view the file and we get the flag.
```
import java.util.*;

class VaultDoorTraining {
    public static void main(String args[]) {
        VaultDoorTraining vaultDoor = new VaultDoorTraining();
        Scanner scanner = new Scanner(System.in); 
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
   }

    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    //
    // -Minion #9567
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_be8d9806f18");
    }
}
```
### **vault-door-1**
Again, view the source code:
```
public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == '9' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == '5' &&
               password.charAt(30) == '2' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == '0' &&
               password.charAt(26) == '7' &&
               password.charAt(31) == 'e';
    }
}
```
This method checks if the content inside `picoCTF{}` matches or not. Arrange the character at the same indexes to obtain the flag.
> NOTE: `charAt()` method returns `true` if the charcater a that index matches with the character in the right side of `==` operator.

### **vault-door-3**
```
public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18g947_u_4_m9r54f");
```
Thw script will give is the flag:
```
string = "jU5t_a_sna_3lpm18g947_u_4_m9r54f"

buffer = [""] * 32


for i in range(8):
    buffer[i] = string[i]

for i in range(8, 16):
    buffer[i] = string[23 - i]

for i in range(16, 32, 2):
    buffer[i] = string[46 - i]


for i in range(31, 16, -2):
    buffer[i] = string[i]

password = "".join(buffer)
print(password)

```
### **vault-door-4**

```
	    106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 070 , 0146,
            '4' , 'a' , '6' , 'c' , 'b' , 'f' , '3' , 'b' ,
```

This is just basic ASCII encoding.
The first row is in decimal and can be converted to text
The second row is in hexadecimal
The third row is in octal

The decoding can be done by:
```
list = [106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  , 0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f, 0o142, 0o131, 0o164, 0o63 , 0o163, 0o137, 0o70 , 0o146]
string = ""

for i in list:
	string = string + chr(i)

string = string + '4a6cbf3b'

print(string)
```
### **vault-door-5**

```
        String urlEncoded = urlEncode(password.getBytes());
        String base64Encoded = base64Encode(urlEncoded.getBytes());
        String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTY1JTMzJTMxJTM1JTMyJTYyJTY2JTM0";
        return base64Encoded.equals(expected)
```

The flag is URL encoded + base64 encoded in order. We can use cyberchef to decode the string `JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVmJTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2JTM0JTVmJTY1JTMzJTMxJTM1JTMyJTYyJTY2JTM0` and we will get the flag

### **vault-door-6**
```
	    0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,
            0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,
            0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,
            0xa , 0x6c, 0x61, 0x6d, 0x37, 0x6d, 0x6d, 0x6d,
```
We have to XOR these bytes with `0x55` and then convert to ASCII to get the flag.

```
bytes= [0x3b, 0x65, 0x21, 0xa , 0x38, 0x0 , 0x36, 0x1d,0xa , 0x3d, 0x61, 0x27, 0x11, 0x66, 0x27, 0xa ,0x21, 0x1d, 0x61, 0x3b, 0xa , 0x2d, 0x65, 0x27,0xa , 0x6c, 0x61, 0x6d, 0x37, 0x6d, 0x6d, 0x6d,]
by=[]

for i in bytes:
	by=by+[i^0x55]
	
string = ''.join(chr(b) for b in by)

print(string)
```
### **vault-door-7**

## **asm series**

### **asm1**

```
	<+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   cmp    DWORD PTR [ebp+0x8],0x3a2
        <+10>:  jg     0x512 <asm1+37>
        <+12>:  cmp    DWORD PTR [ebp+0x8],0x358
        <+19>:  jne    0x50a <asm1+29>
        <+21>:  mov    eax,DWORD PTR [ebp+0x8]
        <+24>:  add    eax,0x12
        <+27>:  jmp    0x529 <asm1+60>
        <+29>:  mov    eax,DWORD PTR [ebp+0x8]
        <+32>:  sub    eax,0x12
        <+35>:  jmp    0x529 <asm1+60>
        <+37>:  cmp    DWORD PTR [ebp+0x8],0x6fa
        <+44>:  jne    0x523 <asm1+54>
        <+46>:  mov    eax,DWORD PTR [ebp+0x8]
        <+49>:  sub    eax,0x12
        <+52>:  jmp    0x529 <asm1+60>
        <+54>:  mov    eax,DWORD PTR [ebp+0x8]
        <+57>:  add    eax,0x12
        <+60>:  pop    ebp
        <+61>:  ret  
```
- The first two lines sets up the stack fram for this function
- The argument passed to this function is `0x6fa`, which will be stored in `DWORD PTR [ebp+0x8]`
- `cmp` compares `0x6fa` with value `0x3a2`
- We can use the `echo $((16#hexvalue))` command to convert the hex values in decimal for comparison.
- `0x6fa` is greater so the next line `jg` will be executed as "jump if greater"
- We are now on label 37. Which compares the value `0x6fa` with itself.
- `jne` or "jump if not equal" will be ignored as it is equal.
- The value `0x6fa` is move to the register `eax` and from it `0x12` is subtracted in the next line.
- `jmp` is the unconditional jump statement and we are now on label 60, after which the the function returns.
- Our flag is `0x6fa-0x12` = `0x6e8`

### **asm2**
```
	<+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   sub    esp,0x10
        <+6>:   mov    eax,DWORD PTR [ebp+0xc]
        <+9>:   mov    DWORD PTR [ebp-0x4],eax
        <+12>:  mov    eax,DWORD PTR [ebp+0x8]
        <+15>:  mov    DWORD PTR [ebp-0x8],eax
        <+18>:  jmp    0x50c <asm2+31>
        <+20>:  add    DWORD PTR [ebp-0x4],0x1
        <+24>:  add    DWORD PTR [ebp-0x8],0xd1
        <+31>:  cmp    DWORD PTR [ebp-0x8],0x5fa1
        <+38>:  jle    0x501 <asm2+20>
        <+40>:  mov    eax,DWORD PTR [ebp-0x4]
        <+43>:  leave  
        <+44>:  ret
```
- The values `(0x4,0x2d)` are passed as argument to the function.
- The first two lines set up the stack frame, and the third line explicitly creates 16bytes of memory for local variables that will be used in the fucntion.
- The value `0x2d` is stored in `[ebp+0xc]` and `0x4` in `[ebp+0x8]`
- In the next four lines the `eax` register is used to store these values in the local variable.
- Now, value `0x2d` is stored in `[ebp-0x4]` and `0x4` in `[ebp-0x8]`
- `jmp` statement , jump to label 31.
- `cmp` is used to compare `0x4` with `0x5fa1` and `jle` jumps to label 20.
- From this line, `add` statement adds `0x1` and `0xd1` to `[ebp-0x4]` and `[ebp-0x8]` respectively and this is a loop. Until the value stored in `[ebp-0x8]` equals or exceeds `0x5fa1` , `0x1` will be added to `0x2d` in every iteration.
```
a = 4
b = 45

while (a<=24481):
	a=a+209
	b=b+1
print(b)
```
- The script prints 163 which is`0xa3` in hex and is our flag.

### **asm3**







































