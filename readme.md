# Dick shell intepreter

[Dick](https://esolangs.org/wiki/Dick) is an esoteric language that has a simple syntax of `OPCODE [PARAM] [PARAM]`.

This syntax pattern allows for the opcodes to be implemented as shell script functions.

## Run

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

## Usage

```shell
> $ dick --help
Usage: dick [options] program.dick

Options:
  --help                     show this help
     -h                      

  --use-strict-mode          enable strict mode; limit to permitted variable names in LongDick.
     -s                      
    --strict                      
    --strict-mode                      

  --no-shebang-args          disable reading arguments from shebang
```

## Language Extension

### Opcodes

#### DRIBBLEDICK modulo arithmatic

`DRIBBLEDICK <operand>` is a _remainder_ or modulo operator, ie, `HAND % <operand>`.

```shell
GRAB 8===D
DRIBBLEDICK 8=====D
PEE # -> 2
```

#### WEE LINE, PEE LINE

`PEE` on it's own prints the number in `HAND`. `WEE` prints the character for the number in `HAND`.  
Use `LINE` parameter to also print a newline character.

```shell
GRAB 8===D
DRIBBLEDICK 8=====D # 3 % 5 = 3
PEE
PEE LINE # -> "33\n"
```

#### WHIP IT OUT

Output ASCII dick to represent the value at hand.  
Can replace 'IT' with a variable name to use the value for that variable.

```shell
GRAB 8===D
HUGEDICK 8=====D # 3 * 5 = 15
WHIP IT OUT # -> "8===============D\n"

DICK four 8====D
WHIP four OUT # -> "8====D\n"
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

### LongDick support

[LongDick](https://esolangs.org/wiki/LongDick) adds a way for conditionals and loops.  

This style of syntax isn't directly executable as a shell script, so requires prepocessing the source.

```shell
COCK GO FAST IF counter IS SMALLER THAN max!
    GRAB counter
    LONGDICK 8=D
    RELEASE counter

    DRIBBLEDICK 8==D
    RELEASE even

    LOOK! even IS JUST LIKE 8D!
        GRAB counter
        PEE LINE
    DICK JOKES ARE IMMATURE, SERIOUSLY
ALRIGHT, STOP COCKING AROUND
```

#### limited variable names

LongDick is supposed to have a limited list of variable names.

>johnson dick cock schlong penis dong

This can be achieved using strict mode.

```shell
> $ dick --strict examples/longdick_list_evens.dick
[ERROR] Invalid variable name 'counter' at examples/longdick_list_evens.dick:04:09
    ... GRIP "small peepee"
    ... RELEASE counter
                ^^^^^^^ 
        variable 'counter' is not one of 'johnson dick cock schlong penis dong'

[ERROR] Invalid variable name 'max' at examples/longdick_list_evens.dick:06:09
    ... GRIP "big peepee"
    ... RELEASE max
                ^^^ 
        variable 'max' is not one of 'johnson dick cock schlong penis dong'
```

## See Also

- [Dick](https://esolangs.org/wiki/Dick) page on esolangs.
- [LongDick](https://esolangs.org/wiki/LongDick) page on esolangs.
- [maximxlss/dick.py](https://github.com/maximxlss/dick.py), a python implementation with some [examples](https://github.com/maximxlss/dick.py/tree/master/examples).

## License

Public domain, or _unlicense_, or CC0... I don't care.