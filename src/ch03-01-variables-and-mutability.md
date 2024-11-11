<!-- warn: "Variables and Mutability" ไม่แน่ใจว่าแปลไทยไปเลยจะตรงกับสิ่งที่จะสื่อหรือเปล่า 
            แต่ก็แปลเป็นไทยไปเลย เพราะไม่ได้เขียนว่า mutable ตรง ๆ  -->
## ตัวแปรและความไม่แน่นอน

อย่างที่ได้กล่าวไว้ในหัวข้อ [“การจัดเก็บค่าด้วยตัวแปร”][storing-values-with-variables]
ตัวแปรจะเป็น immutable (ไม่เปลี่ยนแปลง) โดยค่าเริ่มต้น นี่เป็นหนึ่งในหลาย ๆ วิธีที่ Rust 
ช่วยผลักดันคุณให้เขียนโค้ดที่มีความปลอดภัย และเหมาะกับการทำงานแบบขนาน (concurrency) ได้ง่ายขึ้น
อย่างไรก็ตาม คุณยังคงสามารถเลือกที่จะทำให้ตัวแปรของคุณเป็น mutable (เปลี่ยนแปลงได้) ได้เช่นกัน
มาสำรวจกันว่ายังไงและทำไม Rust จึงสนับสนุนการใช้ตัวแปรแบบ immutable 
และทำไมบางครั้งคุณอาจต้องการตัวแปรแบบ mutable

เมื่อตัวแปรเป็น immutable หลังจากกำหนดค่าให้ตัวแปรในครั้งแรกแล้ว 
คุณไม่สามารถเปลี่ยนค่านั้นได้อีก เพื่อแสดงให้เห็นถึงแนวคิดนี้ สร้างโปรเจกต์ใหม่ชื่อ *variables* 
ในโฟลเดอร์ *projects* โดยใช้คำสั่ง `cargo new variables`

จากนั้น ภายในโฟลเดอร์ *variables* เปิดไฟล์ *src/main.rs* 
และแทนที่โค้ดเดิมทั้งหมดด้วยโค้ดดังต่อไปนี้ ซึ่งจะยังไม่สามารถคอมไพล์ได้:

<span class="filename">ชื่อไฟล์: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/src/main.rs}}
```

บันทึกและรันโปรแกรมโดยใช้คำสั่ง `cargo run` คุณควรได้รับข้อความแสดงข้อผิดพลาดเกี่ยวกับ immutable
ดังที่แสดงในผลลัพธ์นี้:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/output.txt}}
```

ตัวอย่างนี้แสดงให้เห็นว่าคอมไพเลอร์ช่วยคุณค้นหาข้อผิดพลาดในโปรแกรมของคุณได้อย่างไร
ข้อผิดพลาดของคอมไพเลอร์อาจทำให้หงุดหงิด แต่จริง ๆ แล้วข้อผิดพลาดเหล่านี้หมายความว่าโปรแกรมของคุณยังไม่ปลอดภัยมากพอ
ที่จะทำอะไรก็ตามที่คุณอยากทำ ซึ่ง*ไม่*ได้หมายความว่าคุณไม่ใช่โปรแกรมเมอร์ที่ดีแต่อย่างใด!
Rustaceans ที่มีประสบการณ์ก็ยังคงได้รับข้อผิดพลาดจากคอมไพเลอร์

คุณได้รับข้อความแสดงข้อผิดพลาด `` cannot assign twice to immutable variable `x` `` 
เนื่องจากคุณพยายามกำหนดค่าให้กับตัวแปร `x` แบบ immutable เป็นครั้งที่สอง

เป็นเรื่องสำคัญที่เราควรได้รับข้อผิดพลาดขณะคอมไพล์ เมื่อพยายามเปลี่ยนค่าที่ถูกกำหนดให้เป็น immutable
เพราะสถานการณ์เช่นนี้สามารถนำไปสู่ข้อผิดพลาดได้ หากโค้ดส่วนหนึ่งของเราทำงานบนสมมติฐานว่าค่าหนึ่งจะไม่เปลี่ยนแปลง
แต่ส่วนอื่นของโค้ดเปลี่ยนค่าดังกล่าว โค้ดส่วนแรกอาจทำงานผิดพลาดจากที่ออกแบบไว้ 
สาเหตุของข้อผิดพลาดประเภทนี้มักเป็นเรื่องยากที่จะตรวจสอบย้อนหลัง โดยเฉพาะอย่างยิ่งเมื่อโค้ดส่วนที่สองเปลี่ยนค่าเพียงบางค่าเท่านั้น
คอมไพเลอร์ Rust รับประกันว่า เมื่อคุณระบุว่าค่าหนึ่งจะไม่เปลี่ยนแปลง ค่านั้นจะไม่เปลี่ยนแปลงจริง ๆ โดยที่คุณไม่ต้องติดตามเช็คด้วยตัวเอง
โค้ดของคุณจึงง่ายต่อการวิเคราะห์

แต่ mutable นั้นมีประโยชน์มาก และสามารถทำให้การเขียนโค้ดสดวกยิ่งขึ้น แม้ว่าตัวแปรจะเป็น immutable โดยค่าเริ่มต้น
แต่คุณสามารถกำหนดเป็น mutable โดยเพิ่ม `mut` ไว้ข้างหน้าของชื่อตัวแปร ดังที่คุณได้ทำใน 
[บทที่ 2][storing-values-with-variables] การเพิ่ม `mut` ยังสื่อความหมายให้กับผู้อ่านโค้ดในอนาคตด้วย
โดยระบุว่าส่วนอื่น ๆ ของโค้ดจะเปลี่ยนค่าของตัวแปรนี้ได้

ตัวอย่างเช่น ลองเปลี่ยน *src/main.rs* ให้เป็นตามนี้:

<span class="filename">ชื่อไฟล์: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/src/main.rs}}
```

เมื่อเรารันโปรแกรมตอนนี้ เราจะได้ผลลัพธ์ดังนี้:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/output.txt}}
```

เมื่อ `mut` ถูกใช้ เราได้รับอนุญาตให้เปลี่ยนค่าของ `x` จาก `5` เป็น `6` 
ท้ายที่สุดแล้วการตัดสินใจว่าจะใช้ mutable 
หรือไม่นั้นขึ้นอยู่กับคุณและขึ้นอยู่กับสิ่งที่คุณคิดว่าชัดเจนที่สุดในสถานการณ์นั้น

### ค่าคงที่

เช่นเดียวกับตัวแปร immutable ค่าคงที่คือค่าที่กำหนดให้กับตัวแปรและไม่อนุญาตให้เปลี่ยนแปลงค่า
แต่มีความแตกต่างเล็กน้อยระหว่างค่าคงที่และตัวแปร

ข้อแรก คุณไม่สามารถใช้ `mut` กับค่าคงที่ได้ ค่าคงที่ไม่เพียงเป็น immutable โดยค่าเริ่มต้นเท่านั้น
แต่มันเป็น immutable ตลอดไป คุณสามารถประกาศตัวแปรคงที่โดยใช้คีย์เวิร์ด `const` แทนคีย์เวิร์ด 
`let` และ*ต้อง*ระบุประเภทตัวแปร เราจะอธิบายเกี่ยวกับประเภทและการระบุประเภทในหัวข้อถัดไป 
[“ประเภทข้อมูล”][data-types] ดังนั้นไม่ต้องกังวลกับรายละเอียดในตอนนี้
เพียงรู้ว่าคุณต้องระบุประเภทตัวแปรให้กับตัวแปรคงที่เสมอ

ตัวแปรคงที่ สามารถประกาศในขอบเขตใดก็ได้ รวมถึงขอบเขตที่อยู่นอกสุด
ซึ่งทำให้มีประโยชน์สำหรับค่าที่ต้องนำไปใช้กับโค้ดหลายส่วน

ข้อแตกต่างสุดท้ายคือ ตัวแปรคงที่ต้องระบุค่าที่ชัดเจนและคงที่เท่านั้น 
ไม่สามารถเป็นผลลัพธ์จากการคำนวณขณะรันโปรแกรม (runtime)

ต่อไปนี้เป็นตัวอย่างของการประการตัวแปรคงที่:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

The constant’s name is `THREE_HOURS_IN_SECONDS` and its value is set to the
result of multiplying 60 (the number of seconds in a minute) by 60 (the number
of minutes in an hour) by 3 (the number of hours we want to count in this
program). Rust’s naming convention for constants is to use all uppercase with
underscores between words. The compiler is able to evaluate a limited set of
operations at compile time, which lets us choose to write out this value in a
way that’s easier to understand and verify, rather than setting this constant
to the value 10,800. See the [Rust Reference’s section on constant
evaluation][const-eval] for more information on what operations can be used
when declaring constants.

Constants are valid for the entire time a program runs, within the scope in
which they were declared. This property makes constants useful for values in
your application domain that multiple parts of the program might need to know
about, such as the maximum number of points any player of a game is allowed to
earn, or the speed of light.

Naming hardcoded values used throughout your program as constants is useful in
conveying the meaning of that value to future maintainers of the code. It also
helps to have only one place in your code you would need to change if the
hardcoded value needed to be updated in the future.

### Shadowing

As you saw in the guessing game tutorial in [Chapter
2][comparing-the-guess-to-the-secret-number]<!-- ignore -->, you can declare a
new variable with the same name as a previous variable. Rustaceans say that the
first variable is *shadowed* by the second, which means that the second
variable is what the compiler will see when you use the name of the variable.
In effect, the second variable overshadows the first, taking any uses of the
variable name to itself until either it itself is shadowed or the scope ends.
We can shadow a variable by using the same variable’s name and repeating the
use of the `let` keyword as follows:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/src/main.rs}}
```

This program first binds `x` to a value of `5`. Then it creates a new variable
`x` by repeating `let x =`, taking the original value and adding `1` so the
value of `x` is then `6`. Then, within an inner scope created with the curly
brackets, the third `let` statement also shadows `x` and creates a new
variable, multiplying the previous value by `2` to give `x` a value of `12`.
When that scope is over, the inner shadowing ends and `x` returns to being `6`.
When we run this program, it will output the following:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/output.txt}}
```

Shadowing is different from marking a variable as `mut` because we’ll get a
compile-time error if we accidentally try to reassign to this variable without
using the `let` keyword. By using `let`, we can perform a few transformations
on a value but have the variable be immutable after those transformations have
been completed.

The other difference between `mut` and shadowing is that because we’re
effectively creating a new variable when we use the `let` keyword again, we can
change the type of the value but reuse the same name. For example, say our
program asks a user to show how many spaces they want between some text by
inputting space characters, and then we want to store that input as a number:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-04-shadowing-can-change-types/src/main.rs:here}}
```

The first `spaces` variable is a string type and the second `spaces` variable
is a number type. Shadowing thus spares us from having to come up with
different names, such as `spaces_str` and `spaces_num`; instead, we can reuse
the simpler `spaces` name. However, if we try to use `mut` for this, as shown
here, we’ll get a compile-time error:

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/src/main.rs:here}}
```

The error says we’re not allowed to mutate a variable’s type:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/output.txt}}
```

Now that we’ve explored how variables work, let’s look at more data types they
can have.

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[data-types]: ch03-02-data-types.html#ประเภทขอมูล
[storing-values-with-variables]: ch02-00-guessing-game-tutorial.html#การจัดเกบคาดวยตัวแปร
[const-eval]: ../reference/const_eval.html
