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




















