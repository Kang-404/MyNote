## sbit

The **sbit** type defines a bit within a special function register (SFR). It is used in one of the following ways:



```
sbit name = sfr-name ^ bit-position;
sbit name = sfr-address ^ bit-position;
sbit name = sbit-address;
```

Where

| name         | is the name of the SFR bit.                |
| ------------ | ------------------------------------------ |
| sfr-name     | is the name of a previously-defined SFR.   |
| bit-position | is the position of the bit within the SFR. |
| sfr-address  | is the address of an SFR.                  |
| sbit-address | is the address of the SFR bit.             |

With typical 8051 applications, it is often necessary to access individual bits within an SFR. The **sbit** type provides access to bit-addressable SFRs and other bit-addressable objects. For example:



```
sbit EA = 0xAF;
```

This declaration defines **EA** as the SFR bit at address **0xAF**. On the 8051, this is the *enable all* bit in the interrupt enable register.

> ### Note:
>
> - Storage of objects accessed using **sbit** is assumed to be little endian (LSB first). This is the storage format of the [**sfr16**](https://developer.arm.com/documentation/101655/0961/Cx51-User-s-Guide/Language-Extensions/Data-Types/Special-Function-Registers/sfr16?lang=en) type but it is opposite to the storage of [**int**](https://developer.arm.com/documentation/101655/0961/Cx51-User-s-Guide/Language-Extensions/Data-Types/Standard-C-Types/int?lang=en) and **long** data types. Care must be taken when using **sbit** to access bits within standard data types.

Any symbolic name can be used in an **sbit** declaration. The expression to the right of the equal sign ('=') specifies an absolute bit address for the symbolic name. There are three variants for specifying the address:

### Variant 1



```
sbit name = sfr-name ^ bit-position;
```

The previously declared SFR (*sfr-name*) is the base address for the **sbit**. It must be evenly divisible by 8. The *bit-position* (which must be a number from 0-7) follows the carat symbol ('^') and specifies the bit position to access. For example:



```
sfr  PSW = 0xD0;
sfr  IE = 0xA8;

sbit OV = PSW^2;
sbit CY = PSW^7;
sbit EA = IE^7;
```

### Variant 2



```
sbit name = sfr-address ^ bit-position;
```

A character constant (*sfr-address*) specifies the base address for the **sbit**. It must be evenly divisible by 8. The *bit-position* (which must be a number from 0-7) follows the carat symbol ('^') and specifies the bit position to access. For example:



```
sbit OV = 0xD0^2;
sbit CY = 0xD0^7;
sbit EA = 0xA8^7;
```

### Variant 3



```
sbit name = sbit-address;
```

A character constant (*sbit-address*) specifies the address of the **sbit**. It must be a value from 0x80-0xFF. For example:



```
sbit OV = 0xD2;
sbit CY = 0xD7;
sbit EA = 0xAF;
```

> ### Note:
>
> - Not all SFRs are bit-addressable. Only those SFRs whose address is evenly divisible by 8 are bit-addressable. The lower nibble of the SFR's address must be 0 or 8. For example, SFRs at 0xA8 and 0xD0 are bit-addressable, whereas SFRs at 0xC7 and 0xEB are not. To calculate an SFR bit address, add the bit position to the SFR byte address. So, to access bit 6 in the SFR at 0xC8, the SFR bit address would be 0xCE (0xC8 + 6).
> - Special function bits represent an independent declaration class that may not be interchangeable with other bit declarations or bit fields.
> - The **sbit** data type declaration may be used to access individual bits of variables declared with the **bdata** memory type specifier. Refer to [Bit-addressable Objects](https://developer.arm.com/documentation/101655/0961/Cx51-User-s-Guide/Language-Extensions/Data-Types/Bit-Addressable-Objects?lang=en) for more information.
> - **sbit** variables may not be declared inside a function. They must be declared outside of the function body.

来源：[armDeveloper](https://developer.arm.com/documentation/101655/0961/Cx51-User-s-Guide/Language-Extensions/Data-Types/Special-Function-Registers/sbit)

_问题_
``` C
if(P1 ^ 1 == 0){
    ...
}
```
``` C
sbit k1 = P1^1;
if(k1 == 0){
    ...
}
```
上面两段代码有什么区别？
> 在做实验的时候，使用第一段代码会发生乱跳的现象（P1^1乱跳），且若加了`while(P1^1 == 0);`，程序现象会更加奇怪。   
> 使用第二段代码后程序一切正常。

