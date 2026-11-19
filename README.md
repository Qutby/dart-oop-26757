# Dart OOP Assignment: Kigali Bus Card

**Name:** Yasir Altaher Mohammad Ahmad

**Student ID:** 26757

## My numbers
- D = 57, L = 7
- Starting balance = 1570 RWF
- Bus fare = 257 RWF
- Student discount = 17%

## Output of main.dart
Error: name too short
Owner: Yasir | Balance: 1570 RWF
Owner: Yasir Altaher Mohammad Ahmad | Balance: 1570 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 257 RWF
Paid 257 RWF
Owner: Yasir Altaher Mohammad Ahmad | Balance: 3056 RWF
Student discount: 43 RWF
Paid 214 RWF
Owner: Yasir Altaher Mohammad Ahmad | Balance: 1356 RWF
Student card: 17% off


## Part 1: Why no setter for balance?
If balance had a setter, any code could write card.balance = 999999 and give itself free money. With only topUp and pay, the balance can change only by the rules: top-ups must be 500 to 50000 RWF, and a payment can never take it below zero.

## Part 2: What does ~/ do?
print(237 * 17 / 100); prints 40.29 because / is normal division and gives a decimal.
print(237 * 17 ~/ 100); prints 40 because ~/ is integer division: it throws away the decimal part. The discount must be a whole number of RWF, so I use ~/.

## Part 4: Bug table
| Bug | The line | Why it is wrong (my words) | My fix |
|---|---|---|---|
| 1 | Lines 2-3: `String _brand;` and `int _battery;` | Fields that cannot be null need a starting value, and these have none | `String _brand = '';` and `int _battery = 0;` |
| 2 | Line 18: `SmartPhone(...) {` | The parent Phone needs brand and battery, but the child never passes them | Add `: super(brand, battery)` |
| 3 | Lines 22-23: `@override void restart()` | @override needs the parent to have that method, and Phone has no restart | Add `restart()` to Phone |
| 4 | Line 30: `p.battery = 100;` | battery has a getter but no setter | Add a setter that accepts 0 to 100 |
| 5 | Line 31: `print(p.battery());` | battery is a getter, so it is used without () | `print(p.battery);` |
| Not a bug | Line 29: `Phone p = new Phone('Tecno', 50);` | `new` is optional in modern Dart, so the line works | (none) |

## Part 5
My prediction:
It prints 1 and then 5. For Bag a: add() makes items 1, then a.items = -5 is refused because the setter only accepts 0 or more, so it prints 1. For BigBag b: its add() calls super.add() twice, so each add() adds 2. Two calls give 4, then b.items = b.items + 1 makes 5.

Real output:
1
5

Was I right?
Yes, the real output matched my prediction that it's shown in Real output