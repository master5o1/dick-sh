# Dick shell intepreter

[Dick](https://esolangs.org/wiki/Dick) is an esoteric language that has a simple syntax of `OPCODE [PARAM] [PARAM]`.

This syntax pattern allows for the opcodes to be implemented as shell script functions.

## Run

>usage: dick program.dick

```shell
chmod +x ./bin/dick 
./bin/dick  ./examples/fizzbuzz.dick

## add `dick` to path:
export PATH="$PATH:$(pwd)/bin"
## now `dick` is available:
dick ./examples/fizzbuzz.dick

## shebang in fizzbuzz.dick allows direct execution:
chmod +x ./examples/fizzbuzz.dick
./examples/fizzbuzz.dick
```

## Language Extension

### Opcodes

#### DRIBBLEDICK modulo arithmatic

`DRIBBLEDICK <operand>` is a _remainder_ or modulo operator, ie, `HAND % <operand>`.

```shell
GRAB 8===D
DRIBBLEDICK 8=====D
PEE -> 2
```

#### WEE LINE, PEE LINE

`PEE` on it's own prints the number in `HAND`. `WEE` prints the character for the number in `HAND`.  
Use `LINE` parameter to also print a newline character.

```shell
GRAB 8===D
DRIBBLEDICK 8=====D # 3 % 5 = 2
PEE
PEE LINE
## outputs "22\r\n"
```

### Block level
I add three language constructs: loop (`STROKE`), if (`EDGING`), and function (`BAG`).
The inner block makes use of a `<<HEREDOC` string and `eval()` to execute the block.

Indentation must be consistent.

#### STROKE _loop_

STROKE is a while loop. Execute a `<<CUM` block while HAND >= zero.  
i.e., `while [[ $hand -ge 0 ]]; do; ... ; done`


```shell
DICK Z 8==========================================================================================D
DICK A 8=================================================================D

# print chars Z...A
GRAB Z
SMALLDICK A
RELEASE counter
STROKE <<CUM
    RELEASE counter
    LONGDICK A
    WEE
    GRAB counter
    SMALLDICK 8=D
CUM
```

#### EDGING _conditional_

EDGING is an `if statement`. Execute a `<<CUM` block if HAND is zero.  
i.e., `if [[ $hand -eq 0 ]]; then; ... ; fi`

```shell
DICK three 8===D
DICK five 8=====D

DICK F 8======================================================================D
DICK B 8==================================================================D
DICK u 8=====================================================================================================================D
DICK i 8=========================================================================================================D
DICK z 8==========================================================================================================================D

GRAB value
DRIBBLEDICK three
EDGING <<CUM
    GRAB F
    WEE
    GRAB i
    WEE
    GRAB z
    WEE
    GRAB z
    WEE
CUM
```

#### BAG _function_

BAG of Dick operations.  Allows for creating functions or procedures that can be repeatable.

```shell
DICK plus 8===========================================D
DICK equals 8=============================================================D

BAG PRINT_EQUATION operand1 operator operand2 <<END
    GRAB operand1
    PEE
    GRAB operator
    WEE
    GRAB operand2
    PEE
    GRAB equals
    WEE
END

DICK A 8===D
DICK B 8=====D
PRINT_EQUATION A plus B
GRAB A
LONGDICK B
PEE LINE
```

### User Input

#### GRIP _numeric input_

GRIP a number provided by the user. A "🫳" prompts the user to provide a number.  
Input must be in the form of a numeric literal Dick, ie, 8====D.

```shell
GRIP
PEE
```

command line:
```shell
 > $ dick ./examples/function.dick
 🫳 8===D
 🫳 8=====D
3+5=8
3-5=-2
3*5=15
3/5=0
3%5=3
```

## License

Public domain, or _unlicense_, or CC0... I don't care.