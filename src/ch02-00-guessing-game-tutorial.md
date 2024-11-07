# การเขียนโปรแกรม เกมทายตัวเลข

ก้าวเข้าสู่ Rust ด้วยการทำโปรเจกต์ในภาคปฏิบัติกัน! 
ในบทนี้จะแนะนำให้คุณรู้จักกับแนวคิดทั่วไปของ Rust 
โดยแสดงให้คุณเห็นถึงวิธีใช้งานในโปรแกรมจริง
คุณจะได้เรียนรู้เกี่ยวกับ `let`, `match`, method ที่เกี่ยวข้องกับฟังก์ชั่น,
crate และอื่น ๆ ! ในบทต่อไปนี้เราจะสำรวจแนวคิดเหล่านี้ให้ละเอียดยิ่งขึ้น
ในบทนี้คุณจะเพียงฝึกฝนพื้นฐานเท่านั้น 

เราจะใช้เกมทายตัวเลข ซึ่งเป็นปัญหาการเขียนโปรแกรมคลาสสิกสำหรับผู้เริ่มต้น
วิธีการทำงาน: โปรแกรมจะสุ่มตัวเลขจำนวนเต็มขึ้นมา โดยอยู่ในระหว่าง 1 ถึง 100
จากนั้นจะแจ้งให้ผู้เล่นทาย หลังจากป้อนตัวเลขที่ได้ทายแล้ว 
โปรแกรมจะระบุว่าตัวเลขที่ทายนั้นต่ำหรือสูงเกินไป
หากทายถูก เกมจะแสดงข้อความแสดงความยินดี และออกจากโปรแกรม

## สร้างโปรเจกต์ใหม่

ในการสร้างโปรเจกต์ใหม่ ไปที่โฟลเดอร์ *projects* ที่คุณได้สร้างไว้เมื่อบทที่ 1
และสร้างโปรเจกต์ใหม่โดยใช้ Cargo ดังต่อไปนี้:

```console
$ cargo new guessing_game
$ cd guessing_game
```

คำสั่งแรก `cargo new` ใช้ชื่อของโปรเจกต์ (`guessing_game`) เป็น argument แรก
คำสั่งที่สองย้ายไปที่โฟลเดอร์ของโปรเจกต์ใหม่

ดูไฟล์ *Cargo.toml* ทีได้สร้างขึ้น:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial
rm -rf no-listing-01-cargo-new
cargo new no-listing-01-cargo-new --name guessing_game
cd no-listing-01-cargo-new
cargo run > output.txt 2>&1
cd ../../..
-->

<span class="filename">ชื่อไฟล์: Cargo.toml</span>

```toml
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/Cargo.toml}}
```

อย่างที่คุณเห็นไปในบทที่ 1 ซึ่ง `cargo new` ได้สร้างโปรแกรม “Hello, world!” ให้คุณ
ตรวจสอบไฟล์ *src/main.rs*:

<span class="filename">ชื่อไฟล์: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/src/main.rs}}
```

ตอนนี้เรามาคอมไพล์โปรแกรม “Hello, world!” และรันโดยใช้เพียงหนึ่งขั้นตอนด้วยคำสั่ง `cargo run`:

```console
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/output.txt}}
```

คำสั่ง `run` มีประโยชน์เมื่อคุณจำเป็นต้องทำซ้ำอย่างรวดเร็ว (rapidly iterate) ในโปรเจกต์
เช่นเดียวกับที่เราจะทำในเกมนี้ โดยการทดสอบการวนซ้ำแต่ละครั้งอย่างรวดเร็ว 
ก่อนจะไปยังการวนซ้ำถัดไป

เปิดไฟล์ *src/main.rs* ขึ้นมาอีกครั้ง คุณจะเขียนโค้ดทั้งหมดในไฟล์นี้

## การประมวลผลการคาดเดา

ในส่วนแรกของเกมทายตัวเลข เกมจะขอให้ผู้ใช้ป้อนข้อมูล
ประมวลผลข้อมูลนั้น และตรวจสอบว่าข้อมูลนั้นอยู่ในรูปแบบที่ถูกต้องหรือไม่
ในการเริ่มต้นเราจะอนุญาตให้ผู้เล่นป้อนตัวเลขที่คาดเดา พิมพ์โค้ดตามรายการที่ 2-1
บน *src/main.rs*

<Listing number="2-1" file-name="src/main.rs" caption="Code that gets a guess from the user and prints it">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:all}}
```

</Listing>

โค้ดนี้ประกอบไปด้วยข้อมูลจำนวนมาก ดังนั้นเรามาดูกันทีละบรรทัด
ในการรับ input จากผู้ใช้แล้วแสดงผลลัพธ์เป็น output เราจำเป็นต้องนำเข้าไลบารรี input/output `io`
เข้ามามาในขอบเขต โดยไลบรารี `io` มาจากไลบรารีมาตรฐาน ที่รู้จักในชื่อ `std`

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:io}}
```

โดยค่าเริ่มต้น Rust จะนำบางรายการที่กำหนดไว้ในไลบรารีมาตรฐาน เข้ามาไว้ในขอบเขตของทุกโปรแกรม
ซึ่งเรียกว่า *prelude* คุณสามารถดูรายละเอียดทั้งหมดได้
[ในเอกสารคู่มือไลบรารีมาตรฐาน][prelude]

หากสิ่งที่คุณต้องการใช้ไม่อยู่ใน prelude คุณต้องนำเข้าสิ่งนั้นมาไว้ยังขอบเขตที่ชัดเจน
ด้วยคำสั่ง `use` การใช้ไลบรารี `std::io` จะมอบคุณสมบัติมากมายให้กับคุณ 
รวมถึงความสามารถในการรับ input จากผู้ใช้

อย่างที่คุณได้เห็นในบทที่ 1 ฟังก์ชั่น `main` คือจุดเริ่มต้นของโปรแกรม:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:main}}
```

ไวยากรณ์ `fn` จะประกาศฟังก์ชั่นใหม่; วงเล็บ `()` เป็นตัวระบุว่าไม่มี parameters;
และวงเล็บปีกกาเปิด `{` เป็นจุดเริ่มต้นภายในฟังก์ชั่น

อย่างที่คุณได้เรียนรู้ในบทที่ 1 `println!` คือ macro ซึ่งสามารถแสดงข้อความออกทางหน้าจอ:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print}}
```

โค้ดนี้จะแสดงผลข้อความที่แจ้งว่าเกมอะไรและขอให้ผู้ใช้ป้อนข้อมูล

### การจัดเก็บค่าด้วยตัวแปร

ถัดไป เราจะสร้าง *ตัวแปร* ที่เก็บค่าจากผู้ใช้ที่ป้อนเข้ามา ดังต่อไปนี้:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:string}}
```

ตอนนี้โปรแกรมเริ่มน่าสนใจขึ้นแล้ว! มีอีกมากมายที่เกิดขึ้นในบรรทัดเล็ก ๆ นี่
เราใช้คำสั่ง `let` เพื่อประกาศตัวแปร ตรงนี้เป็นอีกหนึ่งตัวอย่าง:

```rust,ignore
let apples = 5;
```

<!-- warn: "immutable" และ "mutable" จะเขียนเป็นภาษาอังกฤษไปเลย 
            แทนที่จะเขียนทับศัพท์หรือแปลไทย เพราะจะได้เกิดความเข้าใจและคุ้นชิ้น  -->

บรรทัดนี้จะประกาศตัวแปรใหม่ชื่อ `apples` และกำหนดค่าเป็น 5 โดยใน Rust ตัวแปรจะมีค่าเริ่มต้นเป็น immutable ซึ่งหมายถึง
หลังจากที่คุณกำหนดค่าให้กับตัวแปรในครั้งแรกแล้ว ค่าจะไม่เปลี่ยนแปลง
เราจะกล่าวถึงรายละเอียดเพิ่มเติมเกี่ยวกับแนวคิดนี้ในหัวข้อ [“ตัวแปรและความไม่แน่นอน”][variables-and-mutability] ของบทที่ 3 
และในการสร้างตัวแปร mutable เราจะเพิ่ม `mut` ไว้หน้าชื่อตัวแปร:

```rust,ignore
let apples = 5; // immutable
let mut bananas = 5; // mutable
```

> หมายเหตุ: ไวยากรณ์ `//` หมายถึงจุดเริ่มต้นของ comment ยาวไปจนจบบรรทัด
> ซึ่ง Rust จะเพิกเฉยกับอะไรก็ตามที่อยู่ใน comment
> เราจะกล่าวถึงรายละเอียดเพิ่มเติมเกี่ยวกับ comment ใน [บทที่ 3][comments]

<!-- warn: ย่อหน้านี้อ่านแล้วดูไม่ลื่นเลย -->
กลับมาที่เกมทายตัวเลข ตอนนี้คุณรู้แล้วว่า `let mut guess` จะสร้างตัวแปร mutable ชื่อ `guess`
ส่วนเครื่องหมายเท่ากับ (`=`) เป็นการบอก Rust ว่าเราต้องการกำหนดค่าบางอย่างให้กับตัวแปร
ทางด้านขวาของเครื่องหมายเท่ากับคือค่าที่กำหนดให้กับตัวแปร `guess` ซึ่งก็คือผลลัพธ์ที่ได้จากการเรียกใช้
`String::new` ที่ return อินสแตนซ์ใหม่ของ `String` 
โดย [`String`][string] ที่กล่าวถึงนี้คือประเภท string ที่อยู่ในไลบรารีมาตรฐาน ที่ซึ่งสามารถขยายขนาดได้
และข้อความถูกเข้ารหัสในรูปแบบ UTF-8

<!-- warn: "type" หากแปลเป็นคำว่า "ประเภท" โดยตรง หรือเขียนเป็นคำอังกฤษตรง ๆ 
           รู้สึกว่ามันยังสื่อความหมายไม่ชัดเจน เลยเขียนเป็น "ประเภทของตัวแปร" -->

ไวยากรณ์ `::` ในบรรทัด `::new` บงชี้ว่า `new` เป็นฟังก์ชั่นที่เกี่ยวข้องกับประเภท `String`
โดย *ฟังก์ชั่นที่เกี่ยวข้อง* หมายถึงฟังก์ชั่นที่ถูกนำไปใช้กับประเภทตัวแปรนั้น ๆ หรือในกรณีนี้ก็คือ `String`
และฟังก์ชั่น `new` ได้สร้าง string เปล่าอันใหม่ขึ้นมา
คุณจะพบฟังก์ชั่น `new` ในหลายประเภทของตัวแปร 
เนื่องจากเป็นชื่อสามัญสำหรับฟังก์ชั่นที่สร้างค่าใหม่ขึ้นมา

คำอธิบายเต็มคือ บรรทัด `let mut guess = String::new();` ได้สร้างตัวแปร mutable 
ที่ถูกกำหนดค่าเป็นอินสแตนซ์ใหม่ของ `String`; หวีว!

### การรับ input จากผู้ใช้

จำได้ว่าเรานำเข้าฟังก์ชั่น input/output จากไลบรารีมาตรฐานด้วย `use std::io;`
ในบรรทัดแรกของโปรแกรม ตอนนี้เราจะเรียกใช้ฟังก์ชั่น `stdin` จากโมดูล `io` 
ซึ่งจะช่วยให้เราสามารถรับค่า input จากผู้ใช้ได้:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:read}}
```

หากเราไม่ได้นำเข้าไลบรารี `io` ด้วย `use std::io;` ที่จุดเริ่มต้นของโปรแกรม
เรายังคงสามารถใช้งานฟังก์ชั่นได้ โดยการเรียกใช้ฟังก์ชั่นแบบนี้ `std::io::stdin`
ฟังก์ชั่น `stdin` จะ return อินสแตนซ์ของ [`std::io::Stdin`][iostdin]
ซึ่งก็คือประเภทของตัวแปรที่สามารถรับ input มาตรฐานสำหรับเทอร์มินัลของคุณ

ถัดไป บรรทัด `.read_line(&mut guess)` จะเรียกใช้ method [`read_line`][read_line]
จากการจัดการ input มาตรฐานเพื่อรับ input จากผู้ใช้ นอกจากนี้เรายังส่ง `&mut guess` เป็น argument
ไปที่ `read_line` เพื่อบอกว่าข้อความจาก input ของผู้ใช้จะเก็บที่ตัวแปรนี้
งานทั้งหมดของ `read_line` คือการนำสิ่งที่ผู้ใช้พิมพ์ไปเป็น input มาตรฐาน และผนวกเข้ากับ string
(โดยไม่ต้องเขียนทับเนื้อหา) ดังนั้นเราจึงสิ่งตัวแปร string ไปเป็น argument
และ argument นั้นต้องเป็น mutable เพื่อให้ method สามารถเปลี่ยนแปลงข้อความใน argument ได้

อักขระ `&` บ่งชี้ว่า argument นั้นเป็น *reference* ซึ่งช่วยให้คุณอนุญาตให้โค้ดหลาย ๆ ส่วน
สามารถเข้าถึงข้อมูลจำนวนหนึ่งโดยไม่จำเป็นต้องคัดลอกข้อมูลนั้นลงในหน่วยความจำหลายครั้ง
*reference* เป็นคุณสมบัติที่ซับซ้อน และเป็นข้อดีหลัก ๆ ข้อหนึ่งของ Rust ที่ช่วยให้ปลอดภัยและง่ายต่อการใช้ reference
คุณไม่จำเป็นต้องรู้รายละเอียดมากมายเพื่อเขียนโปรแกรมนี้ให้สำเร็จ สำหรับตอนนี้ ทั้งหมดที่คุณจำเป็นต้องรู้คือ
reference มีค่าเริ่มต้นเป็น immutable เช่นเดียวกับตัวแปร ดังนั้นคุณต้องเขียน
`&mut guess` แทน `&guess` เพื่อทำให้มันเป็น mutable (บทที่ 4 จะอธิบาย reference ให้ละเอียดมากขึ้น)

<!-- Old heading. Do not remove or links may break. -->
<a id="handling-potential-failure-with-the-result-type"></a>

### การจัดการกับความล้มเหลวที่อาจจะเกิดขึ้นด้วย `Result`

เรายังคงไปกันต่อกับโค้ดในบรรทัดนี้ ขณะนี้เรากำลังกพูดถึงข้อความบรรทัดที่สาม 
แต่โปรดทราบว่าโค้ดสามบรรทัดนี้เป็นส่วนหนึ่งส่วนเดียวกัน
ส่วนถัดไปนี้คือ method:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:expect}}
```

เราสามารถเขียนแบบนี้ได้เช่นกัน:

```rust,ignore
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

อย่างไรก็ตาม หนึ่งบรรทัดยาว ๆ นั้นอ่านยาก ดังนั้นจึงควรแบ่งออกเป็นหลายบรรทัด
บ่อยครั้งที่คุณควรขึ้นบรรทัดใหม่และเว้นวรรค เพื่อช่วยแยกบรรทัดยาว ๆ เมื่อคุณเรียกใช้ method
ด้วยไวยากรณ์ `.method_name()` ตอนนี้เรามาคุยกันว่าบรรทัดนี้ทำอะไร

ตามที่ได้กล่าวไปในข้างต้น `read_line` จะใส่ค่าอะไรก็ตามที่ผู้ใช้ป้อนเข้ามาลงไปในตัวแปร string
ที่เราใส่เข้ามา แตก็จะ return ค่า `Result` ด้วย
โดย [`Result`][result] ก็คือ [*enumeration*][enums] หรือโดยทัวไปเรียกว่า *enum*
ซึ่งเป็นประเภทของตัวแปรที่สามารถเป็นค่าใดค่าหนึ่ง ในหลาย ๆ ค่าที่เป็นไปได้ 
เราเรียกแต่ละค่าที่เป็นไปได้ว่า *variant*

[บทที่ 6][enums] จะคลอบคลุมถึงรายละเอียดเพิ่มเติมเกี่ยวกับ enum 
วัตถุประสงค์ของประเภทตัวแปร `Result` คือการเข้ารหัสข้อมูลเพื่อจัดการข้อผิดพลาด

variant ของ `Result` คือ `Ok` และ `Err` โดย variant `Ok` บงชี้ว่าการดำเนินการสำเร็จ
และภายใน `Ok` คือค่าที่สร้างสำเร็จ variant `Err` หมายถึงการดำเนินการล้มเหลว
และ `Err` ประกอบด้วยข้อมูลที่เกี่ยวกับวิธีการหรือสาเหตุที่การดำเนินการล้มเหลว  

ค่าของประเภทตัวแปร `Result` ก็เหมือนกับประเภทตัวแปรอื่น ๆ ที่มี method ด้วยเช่นกัน
อินสแตนซ์ของ `Result` มี [`expect` method][expect]
ที่คุณสามารถเรียกใช้ได้ หากอินสแตนซ์ของ `Result` นี้คือค่า `Err`
ดังนั้น `expect` จะทำให้โปรแกรมขัดข้อง และแสดงผลข้อความที่คุณใส่เป็น argument ไว้ใน `expect`
หาก method `read_line` มีการ return ค่าเป็น `Err`
มีแนวโน้มว่าจะมีสาเหตุมาจากระบบปฏิบัติการพื้นฐาน
หากอินสแตนซ์ของ `Result` คือค่า `Ok`
`expect` จะดึงค่าที่ `Ok` เก็บไว้ออกมา และ return เฉพาะค่านั้น เพื่อให้คุณสามารถใช้งานได้
ซึ่งในกรณีนี้ค่านั้นคือจำนวนของ byte ที่ถูกใช้ใน input ของผู้ใช้

หากคุณไม่เรียกใช้ `expect` โปรแกรมจะยังคงสามารถคอมไพล์ได้ แต่คุณจะได้รับคำเตือน:

```console
{{#include ../listings/ch02-guessing-game-tutorial/no-listing-02-without-expect/output.txt}}
```

Rust เตือนคุณว่า คุณไม่ได้ใช้งานค่า `Result` ที่ return มาจาก `read_line`
ซึ่งระบุว่าโปรแกรมไม่ได้จัดการกับข้อผิดพลาดที่อาจเกิดขึ้น

วิธีที่ถูกต้องในการจัดการกับคำเตือนคือการเขียนโค้ดจัดการกับข้อผิดพลาด
แต่ในกรณีของเรา เราเพียงต้องการให้โปรแกรมนี้หยุดทำงานเมื่อเกิดปัญหา
ดังนั้นเราจึงสามารถใช้ `expect` ได้ คุณจะได้เรียนรู้เกี่ยวกับการกู้คืนจากข้อผิดพลาดใน 
[บทที่ 9][recover]

<!-- warn: ไม่รู้ว่า "placeholders" ควรจะแปลเป็นไทยว่าอะไรดี เลยไม่ได้ใส่" -->

### การแสดงผลค่าด้วย `println!`

นอกจากวงเล็บปีกกาแล้ว จนถึงขณะนี้ยังมีโค้ดอีกหนึ่งบรรทัดเท่านั้นที่ต้องพูดถึง:

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print_guess}}
```

บรรทัดนี้จะทำการแสดงผลข้อความที่ประกอบไปด้วย input ของผู้ใช้
ชุดเครื่องหมายปีกกา `{}` คือตัวระบุตำแหน่ง: ให้ค้ดว่า `{}` 
เป็นเหมือนคีมจับปูขนาดเล็กที่ยึดค่าต่าง ๆ ไว้กับที่ 
เมื่อต้องการแสดงค่าของตัวแปร สามารถใส่ชื่อตัวแปรลงไปในวงเล็บปีกกาได้
เมื่อต้องการแสดงผลลัพธ์จากการดำเนินการ ใส่วงเล็บปีกกาเปล่าลงในชุดข้อความ
จากนั้นตามด้วยจุลภาค (`,`) ที่คั่นระหว่างตัวดำเนินการต่าง ๆ ตามลำดับเดียวกับวงเล็บปีกกา
การแสดงผลค่าตัวแปรและผลการดำเนินการ โดยเรียกใช้ `println!` ในครั้งเดียว จะมีลักษณะประมาณนี้:

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```

โค้ดนี้จะแสดง `x = 5 and y + 2 = 12`

### การทดสอบในส่วนแรก

มาทดสอบส่วนแรกของเกมทายตัวเลขกัน โดยรันคำสั่ง `cargo run`:


<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-01/
cargo clean
cargo run
input 6 -->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 6.44s
     Running `target/debug/guessing_game`
Guess the number!
Please input your guess.
6
You guessed: 6
```

ในตอนนี้ ส่วนแรกของเกมก็เสร็จเรียบร้อยแล้ว เรากำลังรับ input จากคีย์บอร์ดจากนั้นก็แสดงผลออกมา

## สร้างตัวเลขที่เป็นความลับ

ถัดไป เราจำเป็นต้องสร้างตัวเลขลับเพื่อให้ผู้ใช้พยายามทายให้ถูก ตัวเลขลับควรแตกต่างกันในแต่ละครั้งที่เล่นเกม
เพื่อให้เกมสนุกยิ่งขึ้นหากเล่นหลายครั้ง เราจะใช้ตัวเลขสุ่มระหว่าง 1 ถึง 100 เพื่อให้เกมไม่ยากเกินไป
Rust ไม่มีฟังก์ชั่นสุ่มเลขในไลบรารีมาตรฐาน อย่างไรก็ตามทีมงาน Rust ได้จัดเตรียม [crate `rand`][randcrate]
ที่มีฟังก์ชั่นดังกล่าวไว้แล้ว

### การใช้ crate เพื่อเพิ่มฟังก์ชั่นการใช้งาน

โปรดจำไว้ว่า crate นั้นคือชุดของไฟล์ซอร์สโค้ดของ Rust 
โปรเจกต์ที่เรากำลังสร้างคือ *crate ไบนารี* ซึ่งก็คือไฟล์ที่สามารถรันได้
ส่วน crate `rand` ก็คือ *crate ไลบรารี* ซึ่งบรรจุโค้ดที่ตั้งใจให้ใช้กับโปรแกรมอื่น ๆ และไม่สามารถรันได้ด้วยตัวเอง 

การประสานงานของ Cargo กับ crate ภายนอกคือจุดที่ Cargo โดดเด่นจริง ๆ 
ก่อนที่เราจะเขียนโค้ดโดยใช้ `rand` เราจำเป็นต้องแก้ไขไฟล์ *Cargo.toml* 
เพื่อเพิ่ม crate `rand` ไปยัง dependency โดยทำการเปิดไฟล์ดังกล่าวขึ้นมา
และเพิ่มบรรทัดต่อไปนี้ที่ด้านล่าง ใต้ส่วนหัว `[dependencies]` ที่ Cargo ได้สร้างให้คุณ
ตรวจสอบให้แน่ใจว่าได้ระบุ `rand` แบบเดียวกับที่เราระบุไว้ที่นี่ โดยใช้เวอร์ชั่นเดียวกันนี้
มิฉะนั้น ตัวอย่างโค้ดในบทช่วยสอนนี้อาจใช้การไม่ได้:

<!-- When updating the version of `rand` used, also update the version of
`rand` used in these files so they all match:
* ch07-04-bringing-paths-into-scope-with-the-use-keyword.md
* ch14-03-cargo-workspaces.md
-->

<span class="filename">Filename: Cargo.toml</span>

```toml
{{#include ../listings/ch02-guessing-game-tutorial/listing-02-02/Cargo.toml:8:}}
```

ในไฟล์ *Cargo.toml* ทุกสิ่งทุกอย่างที่ตามหลังส่วนหัวจะเป็นส่วนหนึ่งของส่วนหัว 
ต่อเนื่องไปจนกว่าจะเริ่มส่วนหัวอื่น ๆ โดยใน `[dependencies]`
คุณได้แจ้งให้ Cargo ทราบว่า crate 
ภายนอกที่โปรเจกต์ของคุณจำเป็นต้องใช้และเวอร์ชั่นที่เกี่ยวข้องมีอะไรบ้าง
ในกรณีนี้ เราระบุ crate `rand` พร้อมกับเวอร์ชั่นเชิงความหมาย `0.8.5`
โดย Cargo เข้าใจ[การกำหนดเวอร์ชั่นเชิงความหมาย][semver] (บางครั้งเรียกว่า *SemVer*)
ซึ่งเป็นมาตรฐานในการเขียนหมายเลขเวอร์ชั่น การระบุ `0.8.5` จริง ๆ แล้วคือรูปย่อของ `^0.8.5`
ซึ่งหมายถึงเวอร์ชั่น 0.8.5 หรือใหม่กว่า แต่ต้องต่ำกว่า 0.9.0 ลงมา 

Cargo ถือว่าเวอร์ชั่นเหล่านี้มี API สาธารณะที่เข้ากันได้กับเวอร์ชั่น 0.8.5 
และข้อกำหนดนี้รับประกันว่าคุณจะยังได้รับแพตช์เวอร์ชั่นล่าสุด 
โดยที่ยังสามารถคอมไพล์กับโค้ดในบทนี้ได้ แต่ไม่รับประกันว่าเวอร์ชั่น 0.9.0 หรือสูงกว่าจะมี API เดียวกันกับตัวอย่างต่อไปนี้:

ตอนนี้ เรามาคอมไพล์โปรเจกต์โดยยังไม่ต้องแก้ไขโค้ดใด ๆ ดังที่แสดงในรายการ 2-2

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
rm Cargo.lock
cargo clean
cargo build -->

<Listing number="2-2" caption="The output from running `cargo build` after adding the rand crate as a dependency">

```console
$ cargo build
    Updating crates.io index
  Downloaded rand v0.8.5
  Downloaded libc v0.2.127
  Downloaded getrandom v0.2.7
  Downloaded cfg-if v1.0.0
  Downloaded ppv-lite86 v0.2.16
  Downloaded rand_chacha v0.3.1
  Downloaded rand_core v0.6.3
   Compiling libc v0.2.127
   Compiling getrandom v0.2.7
   Compiling cfg-if v1.0.0
   Compiling ppv-lite86 v0.2.16
   Compiling rand_core v0.6.3
   Compiling rand_chacha v0.3.1
   Compiling rand v0.8.5
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53s
```

</Listing>

คุณอาจจะเห็นหมายเลขเวอร์ชั่นที่ต่างกัน (แต่ทั้งหมดจะเข้ากันได้กับโค้ด ขอบคุณ SemVer!)
และบรรทัดที่ต่างกัน (ขึ้นอยู่กับระบบปฏิบัติการ) และบรรทัดอาจจะอยู่ในลำดับที่ต่างกัน

เมื่อเรานำเข้า dependency ภายนอก Cargo จะทำการดึงทุกสิ่งทุกอย่างในเวอร์ชั่นล่าสุดที่ dependency ต้องการ จาก *registry* ซึ่งเป็นสำเนาของข้อมูลจาก [Crates.io][cratesio]
Crates.io เป็นที่ที่ผู้คนในระบบนิเวศของ Rust โพสต์โปรเจกต์ 
Rust โอเพ่นซอร์ส เพื่อให้คนอื่น ๆ ได้ใช้งาน

หลังจากอัปเดต *registry* แล้ว Cargo จะตรวจสอบส่วน `[dependencies]`
และดาวน์โหลดรายการ crate ใดก็ตามที่ยังไม่ได้ดาวน์โหลด
ในกรณีนี้ แม้ว่าเราจะระบุ `rand` เป็น dependency Cargo ก็ยังดึงเอา crate อื่น ๆ ที่  
`rand` ต้องการมาด้วย หลังจากดาวน์โหลด crate มาแล้ว Rust จะคอมไพล์ crate ทั้งหมดนี้
จากนั้นจึงจะคอมไพล์โปรเจกต์ด้วย dependency ที่มีอยู่

หากคุณรัน `cargo build` อีกครั้งทันที โดยไม่ได้เปลี่ยนแปลงอะไร
คุณจะไม่ได้ผลลัพธ์ใด ๆ นอกจากบรรทัด `Finished` เพราะ Cargo 
ทราบว่าได้ดาวน์โหลด และคอมไพล์ dependency เรียบร้อยแล้ว
และคุณไม่ได้เปลี่ยนแปลงอะไรเกี่ยวกับ dependency ในไฟล์ *Cargo.toml* ของคุณ
Cargo ยังทราบอีกว่าคุณไม่ได้เปลี่ยนแปลงอะไรเกี่ยวกับโค้ดของคุณ
ดังนั้นจึงไม่จำเป็นต้องคอมไพล์ซ้ำอีกครั้ง เมื่อไม่มีอะไรต้องทำมันจึงแค่จบการทำงาน

หากคุณเปิดไฟล์ *src/main.rs* ทำการเปลี่ยนแปลงเล็กน้อยและบันทึก
จากนั้นทำการคอมไพล์อีกครั้ง คุณจะเห็นเพียงผลลัพธ์สองบรรทัดดังนี้:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
touch src/main.rs
cargo build -->

```console
$ cargo build
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53 secs
```

บรรทัดเหล่านี้แสดงให้เห็นว่า Cargo นั้นจะทำการคอมไพล์เพียงโค้ดของคุณเท่านั้น 
ซึ่งได้มีการเปลี่ยนแปลงเล็กน้อยในไฟล์ *src/main.rs* ในขณะที่ dependency 
ของคุณไม่มีการเปลี่ยนแปลง Cargo จึงสามารถนำ dependency เหล่านี้ 
ที่ได้ดาวน์โหลดและคอมไพล์ไว้แล้วมาใช้ซ้ำได้ 

#### การรับประกันการคอมไพล์ซ้ำด้วยไฟล์ *Cargo.lock*

Cargo มีกลไกที่ช่วยให้คุณมั่นใจได้ว่า เมื่อคุณหรือใครก็ตามคอมไพล์โค้ดซ้ำอีกครั้งจะได้ผลลัพธ์เหมือนเดิม:
Cargo จะใช้เฉพาะเวอร์ชั่นของ dependency ที่คุณระบุไว้เท่านั้น จนกว่าคุณจะระบุเป็นอย่างอื่น
ตัวอย่างเช่น สมมติว่าสัปดาห์หน้าเวอร์ชั่น 0.8.6 ของ crate `rand` ได้รับการเผยแพร่
และเวอร์ชั่นดังกล่าวมีการแก้ไขจุดบกพร่องที่สำคัญ แต่ยังมีข้อผิดพลาดซ้ำซ้อนที่จะทำให้โค้ดของคุณเสียหาย
เพื่อรับมือกับปัญหานี้ Rust จะสร้างไฟล์ *Cargo.lock* ในครั้งแรกที่คุณรัน `cargo build`
ดังนั้น ตอนนี้เรามีไฟล์นี้อยู่ในโฟลเดอร์ *guessing_game* แล้ว

เมือคุณคอมไพล์โปรเจกต์เป็นครั้งแรก Cargo จะค้นหาเวอร์ชั่นทั้งหมดของ dependency ที่ตรงตามเกณฑ์
จากนั้นเขียนทั้งหมดลงในไฟล์ *Cargo.lock* เมือคุณคอมไพล์โปรเจกต์ของคุณในอนาคต
Cargo จะเห็นว่ามีไฟล์ *Cargo.lock* อยู่ และจะใช้เวอร์ชั่นที่ระบุไว้ในไฟล์นี้
แทนที่จะทำการค้นหาเวอร์ชั่นของ dependency ซ้ำอีกครั้ง
วิธีนี้จะช่วยให้คุณคอมไพล์ซ้ำได้ได้โดยอัตโนมัติ
กล่าวอีกนัยหนึ่ง โปรเจกต์ของคุณจะยังคงอยู่ในเวอร์ชั่น 0.8.5 จนกว่าคุณจะอัปเกรดโดยชัดเจน
ขอบคุณไฟล์ *Cargo.lock* เนื่องจากไฟล์ *Cargo.lock* มีความสำคัญสำหรับการคอมไพล์ซ้ำ
จึงมักถูกเพิ่มเข้าไปในระบบควบคุมเวอร์ชั่นพร้อมกับโค้ดส่วนอื่น ๆ ในโปรเจกต์ของคุณ 

#### การอัปเดต crate เพื่อรับเวอร์ชั่นใหม่

เมื่อคุณ*ต้องการ*อัปเดต crate Cargo ได้เตรียมคำสั่ง `update` ซึ่งจะไม่สนใจไฟล์ *Cargo.lock*
และทำการค้นหาเวอร์ชั่นล่าสุดที่ตรงตามเงื่อนไขใน *Cargo.toml*
จากนั้น Cargo จะทำการเขียนเวอร์ชั่นเหล่านั้นลงบนไฟล์ *Cargo.lock*
ในกรณีนี้ Cargo จะมองหาเวอร์ชั่นที่สูงกว่า 0.8.5 และต่ำกว่า 0.9.0 เท่านั้น
หาก crate `rand` มีการเผยแพร่สองเวอร์ชั่นคือ 0.8.6 และ 0.9.0
และคุณรันคำสั่ง `cargo update` คุณจะเห็นผลลัพธ์ดังต่อไปนี้:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
cargo update
assuming there is a new 0.8.x version of rand; otherwise use another update
as a guide to creating the hypothetical output shown here -->

```console
$ cargo update
    Updating crates.io index
    Updating rand v0.8.5 -> v0.8.6
```

Cargo ไม่สนใจเวอร์ชั่น 0.9.0 ในจุดนี้ คุณจะสังเกตเห็นการเปลี่ยนแปลงในไฟล์ *Cargo.lock* ของคุณว่า
เวอร์ชั่นของ crate `rand` ที่คุณกำลังใช้คือ 0.8.6
หากต้องการใช้ `rand` เวอร์ชั่น 0.9.0 หรือเวอร์ชั่นใด ๆ ในชุด 0.9.*x*
คุณจะต้องแก้ไขไฟล์ *Cargo.toml* ให้เป็นดังนี้:

```toml
[dependencies]
rand = "0.9.0"
```

ครั้งถัดไปที่คุณรัน `cargo build` Cargo จะอัปเดต registry ของ crate ที่มีอยู่
และประเมินความต้องการของ `rand` ตามเวอร์ชั่นใหม่ที่คุณระบุ

มีเรื่องอื่นๆ มากมายที่จะพูดเกี่ยวกับ [Cargo][doccargo] และ [ecosystem ของมัน][doccratesio]
ซึ่งเราจะกล่าวถึงในบทที่ 14 แต่ในตอนนี้ นั่นคือทั้งหมดที่คุณจำเป็นต้องรู้ 
Cargo จะทำให้การนำไลบรารีกลับมาใช้ใหม่เป็นเรื่องที่ง่ายมาก
ดังนั้น Rustaceans จึงสามารถเขียนโปรเจกต์ขนาดเล็กที่ประกอบขึ้นจากแพ็กเก็จต่าง ๆ ได้

### การสร้างตัวเลขสุ่ม

มาเริ่มใช้ `rand` ในการสุ่มเลขเพื่อทายกัน
ขั้นตอนถัดไปคือการเพิ่มโค้ดลงใน *src/main.rs* ดังที่แสดงในรายการ 2-3

<Listing number="2-3" file-name="src/main.rs" caption="Adding code to generate a random number">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-03/src/main.rs:all}}
```

</Listing>

ขั้นแรก เราเพิ่มบรรทัด `use rand::Rng;` โดย trait `Rng` จะประกาศ method ที่ตัวสร้างตัวเลขสุ่มนำไปใช้
และ trait นี้ต้องอยู่ในขอบเขตเดียวกัน เพื่อให้เราสามารถใช้ method เหล่านั้นได้ บทที่ 10 จะคลอบคลุมถึงรายละเอียดเกี่ยวกับ trait

ถัดไป เราจะเพิ่มสองบรรทัดตรงกลาง ในบรรทัดแรก เราจะเรียกใช้ฟังก์ชั่น `rand::thread_rng` 
เพื่อสร้างตัวสุ่มเลขที่เราจะต้องใช้: ตัวสร้างเลขสุ่มนั้นจะอยู่ในเธรดปัจจุบันที่กำลังทำงาน และถูกกำหนดโดยระบบปฏิบัติการ
จากนั้นเราจะเรียก method `gen_range` จากตัวสร้างเลขสุ่ม method นี้ถูกประกาศโดย trait `Rng`
ที่เราเพิ่มเข้ามาในขอบเขตด้วยบรรทัด `use rand::Rng;`
โดย `gen_range` รับช่วงตัวเลขขอบเขตที่เป็นไปได้ด้วย argument 
และสร้างตัวเลขสุ่มภายในช่วงขอบเขตนั้น ขอบเขตของค่าที่เราใช้นี้มีรูปแบบ `start..=end`
และรวมถึงขอบเขตล่างและบน ดังนั้นเราจึงจำเป็นต้องระบุ `1..=100` เพื่อขอจำนวนระหว่าง 1 ถึง 100

> หมายเหตุ: คุณจะไม่เพียงรู้ว่าต้องใช้ trait ไหน method ไหน และฟังก์ชั่นไหนจาก crate
> ดังนั้นแต่ละ crate จะมีเอกสารคู่มือประกอบการใช้งาน คุณสมบัติเจ๋ง ๆ อีกอย่างหนึ่งของ Cargo
> คือการรันคำสั่ง `cargo doc --open` ซึ่งจะสร้างเอกสารคู่มือจากทุก dependency ของคุณบนเครื่อง
> และเปิดเอกสารบนเบราว์เซอร์ของคุณ ตัวอย่างเช่น หากคุณสนใจฟังก์ชั่นอื่น ๆ ใน crate `rand`
> รันคำสั่ง `cargo doc --open` และคลิก `rand` ในแถบด้านซ้าย

บรรทัดใหม่ลำดับที่สองจะแสดงตัวเลขลับจากการสุ่ม ซึ่งมีประโยชน์ในขณะที่เรากำลังพัฒนาโปรแกรมเพื่อทดสอบ
แต่เราจะลบมันออกในเวอร์ชั่นสุดท้าย คงจะไม่ใช่เกมสักเท่าไหร่หากโปรแกรมแสดงคำตอบทันทีที่เริ่มทำงาน

ลองรันโปรแกรมสักสองสามครั้ง:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-03/
cargo run
4
cargo run
5
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 7
Please input your guess.
4
You guessed: 4

$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 83
Please input your guess.
5
You guessed: 5
```

คุณควรจะได้รับตัวเลขสุ่มที่ต่างกัน และทั้งหมดควรเป็นตัวเลขระหว่าง 1 ถึง 100 เยี่ยมมาก!

## การเปรียบเทียบตัวเลขทายและตัวเลขที่ถูกต้อง

ตอนนี้เรามี input ของผู้ใช้และตัวเลขสุ่มแล้ว เราสามารถเปรียบเทียบมันได้
ขั้นตอนดังกล่าวแสดงอยู่ในรายการ 2-4 โปรดทราบว่าโค้ดนี้จะยังไม่คอมไพล์ตามที่เราได้อธิบาย

<Listing number="2-4" file-name="src/main.rs" caption="Handling the possible return values of comparing two numbers">

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-04/src/main.rs:here}}
```

</Listing>

ขั้นแรก เราเพิ่มคำสั่ง `use` อีกบรรทัด โดยนำเข้าประเภทตัวแปรที่เรียกว่า `std::cmp::Ordering`
เข้ามายังขอบเขตจากไลบรารีมาตรฐาน ประเภทตัวแปร `Ordering` เป็น enum อีกหนึ่งแบบ
และมี variant คือ `Less`, `Greater`, และ `Equal` ซึ่งก็คือผลลัพธ์สามประการที่เป็นไปได้
เมื่องคุณเปรียบเทียบค่าสองค่า

จากนั้นเราจะเพิ่มบรรทัดใหม่ห้าบรรทัดที่ด้านล่าง ซึ่งใช้งานประเภทตัวแปร `Ordering` ที่มี method `cmp`
ที่สามารถเปรียบเทียบค่าสองค่า และสามารถเรียกใช้กับอะไรก็ได้ที่สามารถเปรียบเทียบได้
โดยมันจะอ้างถึงสิ่งที่คุณเปรียบเทียบ: ในที่นี้จะเป็นการเปรียบเทียบ `guess` กับ `secret_number`
จากนั้น return ค่า variant ของ enum `Ordering` ที่เราได้นำเข้ามายังขอบเขตผ่านคำสั่ง `use`
จากนั้นเราใช้ [`match`][match] expression เพื่อตัดสินใจว่าจะทำอย่างไรต่อไป
โดยขึ้นอยู่กับค่า variant ของ `Ordering` ที่ถูก return จากการเรียกใช้ `cmp` 
กับค่าใน `guess` และ `secret_number`

`match` expression ประกอบด้วยแขน และแขนประกอบด้วย*รูป*แบบที่จะจับคู่กัน
และโค้ดที่ควรจะถูกรันเมื่อค่าที่กำหนดตรงกับรูปแบบของแขน Rust จะนำค่าที่กำหนดให้กับ `match`
และตรวจสอบรูปแบบของแขนตามลำดับ รูปแบบและโครงสร้าง `match` เป็นคุณสมบัติที่ทรงพลัง:
ซึ่งช่วยให้คุณสามารถแสดงสถานการณ์ต่าง ๆ ที่โค้ดของคุณอาจพบเจอ และทำให้มั่นใจว่าคุณจะจัดการกับเหตุการณ์เหล่านั้นได้
คุณสมบัติเหล่านี้จะถูกกล่าวถึงโดยละเอียดในบทที่ 6 และบทที่ 19 ตามลำดับ

มาดูตัวอย่างด้วย `match` expression ที่เราใช้ที่นี่
สมมติว่าผู้ใช้ทายหมายเลข 50 และหมายเลขที่สร้างขึ้นแบบสุ่มในครั้งนี้คือ 38

เมื่อโค้ดทำการเปรียบเทียบ 50 กับ 38 method `cmp` จะ return
ค่า `Ordering::Greater` เพราะ 50 นั้นมากกว่า 38 `match` expression จะได้รับค่า
`Ordering::Greater` และเริ่มต้นตรวจสอบรูปแบบของแต่ละแขน
โดยจะเริ่มดูที่แขนแรก `Ordering::Less` และตรวจสอบว่าค่า `Ordering::Greater` 
นั้นไม่ตรงกับ `Ordering::Less` ดังนั้นจึงไม่สนใจโค้ดในแขนนั้น และย้ายไปที่แขนถัดไป
รูปแบบของแขนลำดับถัดไปคือ `Ordering::Greater` ซึ่ง*ตรง*กับ `Ordering::Greater` !
ดังนั้นโค้ดที่เกี่ยวข้องในแขนนี้จะทำงาน และแสดงผล `Too big!` ไปยังหน้าจอ
`match` expression จบการทำงานหลังจากรูปแบบตรงกันในครั้งแรก 
ดังนั้นมันจะไม่ตรวจสอบแขนสุดท้ายในสถานการณ์นี้

อย่างไรก็ตาม โค้ดในรายการที่ 2-4 จะยังไม่สามารถคอมไพล์ มาลองดูกัน:

<!--
The error numbers in this output should be that of the code **WITHOUT** the
anchor or snip comments
-->

```console
{{#include ../listings/ch02-guessing-game-tutorial/listing-02-04/output.txt}}
```

ใจความโดยสรุปของข้อผิดพลาดคือ มี*ประเภทตัวแปรที่ไม่ตรงกัน*
Rust มีระบบประเภทตัวแปรคงที่ที่แข็งแกร่ง อย่างไรก็ตาม มันก็ยังมีการอนุมานประเภทตัวแปร 
เมื่อเราเขียน `let mut guess = String::new()`
Rust สามารถอนุมานได้ว่า `guess` นั้นควรเป็น `String` โดยไม่จำเป็นต้องระบุประเภท
ในทางกลับกัน `secret_number` คือประเภทตัวเลข 
ประเภทตัวแปรของ Rust บางส่วนที่สามารถมีค่าระหว่าง 1 ถึง 100: `i32` คือตัวเลข 32 บิต;
`u32` คือตัวเลขแบบ unsigned 32 บิต; `i64` คือตัวเลข 64 บิต; และอื่น ๆ 
โดยหากไม่ได้ระบุไว้ว่าเป็นประเภทใด Rust จะกำหนดโดยค่าเริ่มต้นเป็น `i32` ซึ่งก็คือประเภทของ `secret_number`
เว้นแต่ว่าจะมีข้อมูลเกี่ยวกับประเภทตัวแปรที่ทำให้ Rust อนุมานเป็นประเภทตัวแปรอื่น
สาเหตุของข้อผิดพลาดคือ Rust ไม่สามารถเปรียบเทียบประเภท string กับตัวเลขได้

ท้ายสุด เราต้องการแปลง `String` ที่โปรแกรมอ่านเป็น input ไปเป็นประเภทตัวเลข
เพื่อให้เราสามารถนำมันไปเปรียบเทียบกับตัวเลขสุ่มได้
โดยเราจะเพิ่มบรรทัดนี้ไปที่ภายในฟังก์ชั่น `main`: 

<span class="filename">ชื่อไฟล์: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/src/main.rs:here}}
```

บรรทัดที่ว่าคือ:

```rust,ignore
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

We create a variable named `guess`. But wait, doesn’t the program already have
a variable named `guess`? It does, but helpfully Rust allows us to shadow the
previous value of `guess` with a new one. *Shadowing* lets us reuse the `guess`
variable name rather than forcing us to create two unique variables, such as
`guess_str` and `guess`, for example. We’ll cover this in more detail in
[Chapter 3][shadowing]<!-- ignore -->, but for now, know that this feature is
often used when you want to convert a value from one type to another type.

We bind this new variable to the expression `guess.trim().parse()`. The `guess`
in the expression refers to the original `guess` variable that contained the
input as a string. The `trim` method on a `String` instance will eliminate any
whitespace at the beginning and end, which we must do to be able to compare the
string to the `u32`, which can only contain numerical data. The user must press
<kbd>enter</kbd> to satisfy `read_line` and input their guess, which adds a
newline character to the string. For example, if the user types <kbd>5</kbd> and
presses <kbd>enter</kbd>, `guess` looks like this: `5\n`. The `\n` represents
“newline.” (On Windows, pressing <kbd>enter</kbd> results in a carriage return
and a newline, `\r\n`.) The `trim` method eliminates `\n` or `\r\n`, resulting
in just `5`.

The [`parse` method on strings][parse]<!-- ignore --> converts a string to
another type. Here, we use it to convert from a string to a number. We need to
tell Rust the exact number type we want by using `let guess: u32`. The colon
(`:`) after `guess` tells Rust we’ll annotate the variable’s type. Rust has a
few built-in number types; the `u32` seen here is an unsigned, 32-bit integer.
It’s a good default choice for a small positive number. You’ll learn about
other number types in [Chapter 3][integers]<!-- ignore -->.

Additionally, the `u32` annotation in this example program and the comparison
with `secret_number` means Rust will infer that `secret_number` should be a
`u32` as well. So now the comparison will be between two values of the same
type!

The `parse` method will only work on characters that can logically be converted
into numbers and so can easily cause errors. If, for example, the string
contained `A👍%`, there would be no way to convert that to a number. Because it
might fail, the `parse` method returns a `Result` type, much as the `read_line`
method does (discussed earlier in [“Handling Potential Failure with
`Result`”](#handling-potential-failure-with-result)<!-- ignore-->). We’ll treat
this `Result` the same way by using the `expect` method again. If `parse`
returns an `Err` `Result` variant because it couldn’t create a number from the
string, the `expect` call will crash the game and print the message we give it.
If `parse` can successfully convert the string to a number, it will return the
`Ok` variant of `Result`, and `expect` will return the number that we want from
the `Ok` value.

Let’s run the program now:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/
cargo run
  76
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.43s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 58
Please input your guess.
  76
You guessed: 76
Too big!
```

Nice! Even though spaces were added before the guess, the program still figured
out that the user guessed 76. Run the program a few times to verify the
different behavior with different kinds of input: guess the number correctly,
guess a number that is too high, and guess a number that is too low.

We have most of the game working now, but the user can make only one guess.
Let’s change that by adding a loop!

## Allowing Multiple Guesses with Looping

The `loop` keyword creates an infinite loop. We’ll add a loop to give users
more chances at guessing the number:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-04-looping/src/main.rs:here}}
```

As you can see, we’ve moved everything from the guess input prompt onward into
a loop. Be sure to indent the lines inside the loop another four spaces each
and run the program again. The program will now ask for another guess forever,
which actually introduces a new problem. It doesn’t seem like the user can quit!

The user could always interrupt the program by using the keyboard shortcut
<kbd>ctrl</kbd>-<kbd>c</kbd>. But there’s another way to escape this insatiable
monster, as mentioned in the `parse` discussion in [“Comparing the Guess to the
Secret Number”](#comparing-the-guess-to-the-secret-number)<!-- ignore -->: if
the user enters a non-number answer, the program will crash. We can take
advantage of that to allow the user to quit, as shown here:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-04-looping/
cargo run
(too small guess)
(too big guess)
(correct guess)
quit
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 1.50s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 59
Please input your guess.
45
You guessed: 45
Too small!
Please input your guess.
60
You guessed: 60
Too big!
Please input your guess.
59
You guessed: 59
You win!
Please input your guess.
quit
thread 'main' panicked at 'Please type a number!: ParseIntError { kind: InvalidDigit }', src/main.rs:28:47
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Typing `quit` will quit the game, but as you’ll notice, so will entering any
other non-number input. This is suboptimal, to say the least; we want the game
to also stop when the correct number is guessed.

### Quitting After a Correct Guess

Let’s program the game to quit when the user wins by adding a `break` statement:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/no-listing-05-quitting/src/main.rs:here}}
```

Adding the `break` line after `You win!` makes the program exit the loop when
the user guesses the secret number correctly. Exiting the loop also means
exiting the program, because the loop is the last part of `main`.

### Handling Invalid Input

To further refine the game’s behavior, rather than crashing the program when
the user inputs a non-number, let’s make the game ignore a non-number so the
user can continue guessing. We can do that by altering the line where `guess`
is converted from a `String` to a `u32`, as shown in Listing 2-5.

<Listing number="2-5" file-name="src/main.rs" caption="Ignoring a non-number guess and asking for another guess instead of crashing the program">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-05/src/main.rs:here}}
```

</Listing>

We switch from an `expect` call to a `match` expression to move from crashing
on an error to handling the error. Remember that `parse` returns a `Result`
type and `Result` is an enum that has the variants `Ok` and `Err`. We’re using
a `match` expression here, as we did with the `Ordering` result of the `cmp`
method.

If `parse` is able to successfully turn the string into a number, it will
return an `Ok` value that contains the resultant number. That `Ok` value will
match the first arm’s pattern, and the `match` expression will just return the
`num` value that `parse` produced and put inside the `Ok` value. That number
will end up right where we want it in the new `guess` variable we’re creating.

If `parse` is *not* able to turn the string into a number, it will return an
`Err` value that contains more information about the error. The `Err` value
does not match the `Ok(num)` pattern in the first `match` arm, but it does
match the `Err(_)` pattern in the second arm. The underscore, `_`, is a
catchall value; in this example, we’re saying we want to match all `Err`
values, no matter what information they have inside them. So the program will
execute the second arm’s code, `continue`, which tells the program to go to the
next iteration of the `loop` and ask for another guess. So, effectively, the
program ignores all errors that `parse` might encounter!

Now everything in the program should work as expected. Let’s try it:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-05/
cargo run
(too small guess)
(too big guess)
foo
(correct guess)
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 4.45s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 61
Please input your guess.
10
You guessed: 10
Too small!
Please input your guess.
99
You guessed: 99
Too big!
Please input your guess.
foo
Please input your guess.
61
You guessed: 61
You win!
```

Awesome! With one tiny final tweak, we will finish the guessing game. Recall
that the program is still printing the secret number. That worked well for
testing, but it ruins the game. Let’s delete the `println!` that outputs the
secret number. Listing 2-6 shows the final code.

<Listing number="2-6" file-name="src/main.rs" caption="Complete guessing game code">

```rust,ignore
{{#rustdoc_include ../listings/ch02-guessing-game-tutorial/listing-02-06/src/main.rs}}
```

</Listing>

At this point, you’ve successfully built the guessing game. Congratulations!

## Summary

This project was a hands-on way to introduce you to many new Rust concepts:
`let`, `match`, functions, the use of external crates, and more. In the next
few chapters, you’ll learn about these concepts in more detail. Chapter 3
covers concepts that most programming languages have, such as variables, data
types, and functions, and shows how to use them in Rust. Chapter 4 explores
ownership, a feature that makes Rust different from other languages. Chapter 5
discusses structs and method syntax, and Chapter 6 explains how enums work.

[prelude]: https://doc.rust-lang.org/std/prelude/index.html
[variables-and-mutability]: ch03-01-variables-and-mutability.html#ตัวแปรและความไมแนนอน
[comments]: ch03-04-comments.html
[string]: https://doc.rust-lang.org/std/string/struct.String.html
[iostdin]: https://doc.rust-lang.org/std/io/struct.Stdin.html
[read_line]: https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_line
[result]: https://doc.rust-lang.org/std/result/enum.Result.html
[enums]: ch06-00-enums.html
[expect]: https://doc.rust-lang.org/std/result/enum.Result.html#method.expect
[recover]: ch09-02-recoverable-errors-with-result.html
[randcrate]: https://crates.io/crates/rand
[semver]: http://semver.org
[cratesio]: https://crates.io/
[doccargo]: https://doc.rust-lang.org/cargo/
[doccratesio]: https://doc.rust-lang.org/cargo/reference/publishing.html
[match]: ch06-02-match.html
[shadowing]: ch03-01-variables-and-mutability.html#shadowing
[parse]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[integers]: ch03-02-data-types.html#integer-types
