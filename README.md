<div align="center">

## Porting of Credit Card Number Check and Type Ident


</div>

### Description


 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jonathan Tew](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jonathan-tew.md)
**Level**          |Unknown
**User Rating**    |4.8 (19 globes from 4 users)
**Compatibility**  |Java \(JDK 1\.1\)
**Category**       |[Classes](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/classes__2-83.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jonathan-tew-porting-of-credit-card-number-check-and-type-ident__2-263/archive/master.zip)





### Source Code

```
/*
 Source code ported by Jonathan Tew (jtew@ixworld.com) from VB to Java.
 Original code module credits:
 Name: Credit Card Identification
 Description: Determines type of Credit Card by it's number.
 By: John Anderson
 Name: Credit Card Checksum Checker
 Description:Checks to see if a Credit Card Number is valid
          by performing the LUHN-10 check on it.
 By: John Anderson
*/
public class CreditCardVerify {
 public static final int CARDTYPE_UNKNOWN = 0;
 public static final int CARDTYPE_VISA = 1;
 public static final int CARDTYPE_AMEX = 2;
 public static final int CARDTYPE_DINERSCLUB = 3;
 public static final int CARDTYPE_JCB = 4;
 public static final int CARDTYPE_DISCOVER = 5;
 public static final int CARDTYPE_ENROUTE = 6;
 public static final int CARDTYPE_MASTERCARD = 7;
 public static boolean isValidCCNum(String ccNum) {
  int i;
  int total = 0;
  String tempMultiplier = "";
  for (i = ccNum.length(); i >= 2; i -= 2) {
   total = total + cint(ccNum.charAt(i - 1));
   tempMultiplier = "" + (cint(ccNum.charAt(i - 2)) * 2);
   total = total + cint(left(tempMultiplier));
   if (tempMultiplier.length() > 1) {
    total = total + cint(right(tempMultiplier));
   }
  }
  if (ccNum.length() % 2 == 1) {
   total = total + cint(left(ccNum));
  }
  if (total % 10 == 0) return(true);
   else return(false);
 }
 private static char left(String s) {
  return(s.charAt(0));
 }
 private static char right(String s) {
  return(s.charAt(s.length() - 1));
 }
 private static int cint(char ch) {
  if (ch == '0') return(0);
  if (ch == '1') return(1);
  if (ch == '2') return(2);
  if (ch == '3') return(3);
  if (ch == '4') return(4);
  if (ch == '5') return(5);
  if (ch == '6') return(6);
  if (ch == '7') return(7);
  if (ch == '8') return(8);
  if (ch == '9') return(9);
  // Should never get here, but oh well
  return(0);
 }
 public static int cardType(String ccNum) {
  String header = "";
  switch (left(ccNum)) {
   case '5' :
    header = ccNum.substring(0, 2);
         if (Integer.parseInt(header) >= 51 && Integer.parseInt(header) <= 55 && ccNum.length() == 16) {
          return(CARDTYPE_MASTERCARD);
         }
         break;
   case '4' :
         if (ccNum.length() == 13 || ccNum.length() == 16) {
          return(CARDTYPE_VISA);
         }
         break;
   case '3' :
         header = ccNum.substring(0, 3);
         if (Integer.parseInt(header) >= 340 && Integer.parseInt(header) <= 379 && ccNum.length() == 15) {
          return(CARDTYPE_AMEX);
         }
         if (Integer.parseInt(header) >= 300 && Integer.parseInt(header) <= 305 && ccNum.length() == 14) {
          return(CARDTYPE_DINERSCLUB);
         }
         if (Integer.parseInt(header) >= 360 && Integer.parseInt(header) <= 368 && ccNum.length() == 14) {
          return(CARDTYPE_DINERSCLUB);
         }
         if (Integer.parseInt(header) >= 380 && Integer.parseInt(header) <= 389 && ccNum.length() == 14) {
          return(CARDTYPE_DINERSCLUB);
         }
         if (Integer.parseInt(header) >= 300 && Integer.parseInt(header) <= 399 && ccNum.length() == 16) {
          return(CARDTYPE_JCB);
         }
         break;
   case '6' :
         header = ccNum.substring(0, 4);
         if (Integer.parseInt(header) == 6011 && ccNum.length() == 16) {
          return(CARDTYPE_DISCOVER);
         }
         break;
   case '2' :
         header = ccNum.substring(0, 4);
         if ((Integer.parseInt(header) == 2014 || Integer.parseInt(header) == 2149) && ccNum.length() == 15) {
          return(CARDTYPE_ENROUTE);
         }
         if (Integer.parseInt(header) == 2131 && ccNum.length() == 15) {
          return(CARDTYPE_JCB);
         }
         break;
   case '1' :
         header = ccNum.substring(0, 4);
         if (Integer.parseInt(header) == 1800 && ccNum.length() == 15) {
          return(CARDTYPE_JCB);
         }
         break;
  }
  return(CARDTYPE_UNKNOWN);
 }
}
```

