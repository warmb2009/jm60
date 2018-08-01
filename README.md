JM60
======================
[外设堂地址](http://www.weistang.com/thread-99784-1-1.html)
## 外壳及其他
	使用104机械键盘, 锯钢板, 锯pcb板. 手艺好的可以锯掉外壳后, 再拼接为完整外壳.
	贱猫原版用的是gh60外壳, 然后pcb按照gh60原装位置进行打孔.
## 开发板为 Arduino Pro Micro (淘宝20+一片, 18个IO, 用5x13矩阵, 无灯gh60)
### 改动的文件为 
	config.h(更改为5x13矩阵)
	keymap_common.h 
	keymap_poker.h (更改键盘按键及层阵列)
	matrix.c (矩阵扫描程序, 更改所使用引脚)
	led.c (注视掉led灯控代码)
	
	修改自tmk_keyboard/keyboard/gm60
### 针脚:
	行引脚定义
		row:  0   1   2   3   4
		pin :  D3  D2  D1  D0  D4

	列引脚定义
		col:  0   1   2   3   4   5   6   7   8   9   10  11  12
		pin:  C6  D7  E6  B4  B5  B6  B2  B3  B1  F7  F6  F5  F4

### 使用方法
	短接rst及接地两次
	$ make
	$ sudo avrdude -p atmega32u4 -P /dev/ttyACM0 -c avr109 -b 57600 -U flash:w:gh60_lufa.hex
GH60 keyboard firmware
======================
DIY compact keyboard designed and run by komar007 and Geekhack community.

- Both Rev.A and Rev.B PCB are supported by one firmware binary(issue #64)

## GH60 Resources
- [KOMAR's project page](http://blog.komar.be/projects/gh60-programmable-keyboard/)
- [Prototyping](http://geekhack.org/index.php?topic=34959.0)
- [Rev.A PCB test](http://geekhack.org/index.php?topic=37570.0)
- [Rev.B PCB test](http://geekhack.org/index.php?topic=50685.0)
- [Group buy](http://geekhack.org/index.php?topic=41464.0)


## Build
Move to this directory then just run `make` like:

    $ make

Use `make -f Makefile.pjrc` if you want to use PJRC stack but I find no reason to do so now.


## Keymap
Several version of keymap are available in advance but you are recommended to define your favorite layout yourself. To define your own keymap create file named `keymap_<name>.c` and see keymap document(you can find in top README.md) and existent keymap files.

To build firmware binary hex file with a certain keymap just do `make` with `KEYMAP` option like:

    $ make KEYMAP=[poker|poker_set|poker_bit|plain|hasu|spacefn|hhkb|<name>]


### 1  Poker
[keymap_poker.c](keymap_poker.c) emulates original Poker layers
while both [keymap_poker_bit.c](keymap_poker_bit.c) and [keymap_poker_set.c](keymap_poker_set.c) implements same layout in different way and they fix a minor issue of original Poker and enhance arrow keys.

    Fn + Esc = `
    Fn + {left, down, up, right}  = {home, pgdown, pgup, end}

#### 1.0 Default layer
    ,-----------------------------------------------------------.
    |  `|  1|  2|  3|  4|  5|  6|  7|  8|  9|  0|  -|  =|Backsp |
    |-----------------------------------------------------------|
    |Tab  |  Q|  W|  E|  R|  T|  Y|  U|  I|  O|  P|  [|  ]|    \|
    |-----------------------------------------------------------|
    |Caps  |  A|  S|  D|  F|  G|  H|  J|  K|  L|  ;|  '|Return  |
    |-----------------------------------------------------------|
    |Shift   |  Z|  X|  C|  V|  B|  N|  M|  ,|  .|  /|Shift     |
    |-----------------------------------------------------------|
    |Ctrl|Gui |Alt |      Space             |Fn  |Gui |App |Ctrl|
    `-----------------------------------------------------------'
#### 1.1 Poker Fn layer
    ,-----------------------------------------------------------.
    |Esc| F1| F2| F3| F4| F5| F6| F7| F8| F9|F10|F11|F12|       |
    |-----------------------------------------------------------|
    |     |FnQ| Up|   |   |   |   |   |   |Cal|   |Hom|Ins|     |
    |-----------------------------------------------------------|
    |      |Lef|Dow|Rig|   |   |Psc|Slk|Pau|   |Tsk|End|        |
    |-----------------------------------------------------------|
    |        |Del|   |Web|Mut|VoU|VoD|   |PgU|PgD|Del|   Up     |
    |-----------------------------------------------------------|
    |    |    |    |         FnS            |Fn  |Left|Down|Righ|
    `-----------------------------------------------------------'


### 2. Plain
Without any Fn layer this will be useful if you want to use key remapping tool like AHK on host.
See [keymap_plain.c](keymap_plain.c) for detail.

#### 1.0 Plain Default layer
    ,-----------------------------------------------------------.
    |Esc|  1|  2|  3|  4|  5|  6|  7|  8|  9|  0|  -|  =|Backsp |
    |-----------------------------------------------------------|
    |Tab  |  Q|  W|  E|  R|  T|  Y|  U|  I|  O|  P|  [|  ]|    \|
    |-----------------------------------------------------------|
    |Caps  |  A|  S|  D|  F|  G|  H|  J|  K|  L|  ;|  '|Return  |
    |-----------------------------------------------------------|
    |Shift   |  Z|  X|  C|  V|  B|  N|  M|  ,|  .|  /|Shift     |
    |-----------------------------------------------------------|
    |Ctrl|Gui |Alt |      Space             |Alt |Gui |App |Ctrl|
    `-----------------------------------------------------------'


### 3. Hasu
This is my favorite keymap with HHKB Fn, Vi cursor and Mousekey layer. See [keymap_hasu.c](keymap_hasu.c) for detail.


### 4. SpaceFN
This layout proposed by spiceBar uses space bar to change layer with using Dual role key technique. See [keymap_spacefn.c](keymap_spacefn.c) and [SpaceFN discussion](http://geekhack.org/index.php?topic=51069.0).

#### 4.0 Default layer
    ,-----------------------------------------------------------.
    |Esc|  1|  2|  3|  4|  5|  6|  7|  8|  9|  0|  -|  =|Backsp |
    |-----------------------------------------------------------|
    |Tab  |  Q|  W|  E|  R|  T|  Y|  U|  I|  O|  P|  [|  ]|    \|
    |-----------------------------------------------------------|
    |Caps  |  A|  S|  D|  F|  G|  H|  J|  K|  L|  ;|  '|Return  |
    |-----------------------------------------------------------|
    |Shift   |  Z|  X|  C|  V|  B|  N|  M|  ,|  .|  /|Shift     |
    |-----------------------------------------------------------|
    |Ctrl|Gui |Alt |      Space/Fn          |Alt |Gui |App |Ctrl|
    `-----------------------------------------------------------'
#### 4.1 SpaceFN layer
    ,-----------------------------------------------------------.
    |`  | F1| F2| F3| F4| F5| F6| F7| F8| F9|F10|F11|F12|Delete |
    |-----------------------------------------------------------|
    |     |   |   |   |   |   |   |Hom|Up |End|Psc|Slk|Pau|Ins  |
    |-----------------------------------------------------------|
    |      |   |   |   |   |   |PgU|Lef|Dow|Rig|   |   |        |
    |-----------------------------------------------------------|
    |        |   |   |   |   |Spc|PgD|`  |~  |   |   |          |
    |-----------------------------------------------------------|
    |    |    |    |            Fn          |    |    |    |    |
    `-----------------------------------------------------------'


### 5. HHKB
[keymap_hhkb.c](keymap_hhkb.c) emulates original HHKB layers.
#### 5.0: Default layer
    ,-----------------------------------------------------------.
    |Esc|  1|  2|  3|  4|  5|  6|  7|  8|  9|  0|  -|  =|  \|  `|
    |-----------------------------------------------------------|
    |Tab  |  Q|  W|  E|  R|  T|  Y|  U|  I|  O|  P|  [|  ]|Bspc |
    |-----------------------------------------------------------|
    |Ctrl  |  A|  S|  D|  F|  G|  H|  J|  K|  L|Fn3|  '|Return  |
    |-----------------------------------------------------------|
    |Shift   |  Z|  X|  C|  V|  B|  N|  M|  ,|  .|  /|Shift |Fn |
    |-----------------------------------------------------------|
    |    |Gui |Alt |      Space             |    |Alt |Gui |    |
    `-----------------------------------------------------------'
#### 5.1: HHKB Fn layer
    ,-----------------------------------------------------------.
    |Pwr| F1| F2| F3| F4| F5| F6| F7| F8| F9|F10|F11|F12|Ins|Del|
    |-----------------------------------------------------------|
    |Caps |   |   |   |   |   |   |   |Psc|Slk|Pus|Up |   |     |
    |-----------------------------------------------------------|
    |      |VoD|VoU|Mut|Ejc|   |  *|  /|Hom|PgU|Lef|Rig|Enter   |
    |-----------------------------------------------------------|
    |        |   |   |   |   |   |  +|  -|End|PgD|Dow|      |   |
    |-----------------------------------------------------------|
    |    |    |    |                        |    |    |    |    |
    `-----------------------------------------------------------'

