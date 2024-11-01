## Hello, World!

หลังจากที่คุณติดตั้ง Rust แล้ว ก็ถึงเวลาที่คุณจะได้สร้างโปรแกรมแรกของคุณเอง
เป็นเรื่องปกติในการเรียนรู้ภาษาใหม่ที่จะได้สร้างโปรแกรมเล็ก ๆ ที่แสดงข้อความ `Hello, world!` บนหน้าจอ ดังนั้นเราก็จะทำแบบเดียวกันที่นี่!

> หมายเหตุ: หนังสือเล่มนี้ถือว่าคุณมีความคุ้นเคยอยู่บ้างเกี่ยวกับการใช้งานบรรทัดคำสั่ง
> Rust ไม่ได้กำหนดความต้องการเฉพาะเจาะจงเกี่ยวกับการแก้ไข เครื่องมือ หรือต่ำแหน่งของโค้ด
> ดังนั้น หากคุณต้องการใช้สภาพแวดล้อมสำหรับการพัฒนาแบบเบ็ดเสร็จ (IDE) แทนบรรทัดคำสั่ง
> คุณสามารถเลือกใช้ IDE ที่คุณชื่นชอบได้ตามสบาย ปัจจุบัน IDE จำนวนมากรองรับ 
> Rust ในระดับหนึ่งแล้ว ตรวจสอบเอกสารคู่มือของ IDE เพื่อดูรายละเอียด 
> ทีมงานของ Rust มุ่งเน้นไปที่การเปิดทางให้ IDE อันยอดเยี่ยมรองรับผ่าน `rust-analyzer`
> ไปที่ [Appendix D][devtools]<!-- ignore --> เพื่อดูรายละเอียดเพิ่มเติม

### การสร้างโฟลเดอร์สำหรับโปรเจกต์

คุณจะเริ่มต้นด้วยการสร้าโฟลเดอร์สำหรับเก็บโค้ด Rust ของคุณ 
ไม่สำคัญว่าโค้ดของคุณจะอยู่ในโฟลเดอร์ไหน
แต่ในแบบฝึกหัดและโปรเจกต์ในหนังสือเล่มนี้ 
เราแนะนำให้สร้างโฟลเดอร์ชื่อ *projects* ไว้ในโฟลเดอร์โฮมของคุณ 
และเก็บโปรเจกต์ทั้งหมดของคุณไว้ที่นั่น

เปิดเทอร์มินัลและรันคำสั่งต่อไปนี้ เพื่อสร้างโฟลเดอร์ที่ชื่อ *projects* และโฟลเดอร์สำหรับโปรเจกต์ 
“Hello, world!” ที่อยู่ภายในโฟลเดอร์ *projects*

สำหรับ Linux MacOS และ PowerShell บน Windows ใช้คำสั่งนี้:

```console
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

สำหรับ Windows CMD ใช้คำสั่งนี้:

```cmd
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

### การเขียนและการรันโปรแกรม Rust

จากนั้นสร้างไฟล์ต้นฉบับโดยตั้งชื่อว่า *main.rs* โดยไฟล์โค้ด Rust จะลงท้ายด้วยนามสกุล *.rs* เสมอ
หากชื่อไฟล์ของคุณมีมากกว่าหนึ่งคำ ให้คั่นระหว่างคำด้วยเครื่องหมายขีดล่าง
ตัวอย่างเช่น ใช้ *hello_world.rs* แทน *helloworld.rs* 

จากนั้นเปิดไฟล์ *main.rs* ที่คุณเพิ่งสร้างไป และเขียนโค้ดตามรายการที่ 1-1

<Listing number="1-1" file-name="main.rs" caption="A program that prints `Hello, world!`">

```rust
fn main() {
    println!("Hello, world!");
}
```

</Listing>

บันทึกไฟล์ จากนั้นกลับไปที่เทอร์มินัลของคุณในโฟลเดอร์ *~/projects/hello_world* 
บน Linux หรือ MacOS รันคำสั่งต่อไปนี้เพื่อคอมไพล์และรันไฟล์:

```console
$ rustc main.rs
$ ./main
Hello, world!
```

บน Windows รันคำสั่ง `.\main.exe` แทนคำสั่ง `./main`:

```powershell
> rustc main.rs
> .\main.exe
Hello, world!
```

ไม่ว่าคุณจะใช้ระบบปฏิบัติการใด ข้อความ `Hello, world!` ควรแสดงผลบนเทอร์มินัล
หากคุณไม่เห็นผลลัพธ์นี้ โปรดกลับไปที่ส่วน [“การแก้ไขปัญหา”][troubleshooting] ในบทการติดตั้ง
สำหรับช่องทางในการขอความช่วยเหลือ

หาก `Hello, world!` แสดงผล ยินดีด้วย! คุณได้เขียนโปรแกรม Rust อย่างเป็นทางการแล้ว
และนั่นทำให้คุณเป็นโปรแกรมเมอร์ของ Rust ยินดีต้อนรับ!

### กายวิภาคของ Rust

เรามาทบทวนรายละเอียดของโปรแกรม “Hello, world!” กัน
และนี่คือปริศนาชิ้นแรก:

```rust
fn main() {

}
```

บรรทัดเหล่านี้ประกาศฟังก์ชั่นชื่อ `main` โดยฟังก์ชั่น `main` 
มีความพิเศษคือ จะเป็นส่วนแรกที่เริ่มทำงานในทุกโปรแกรมที่เขียนด้วย Rust
โดยบรรทัดแรกที่ได้ประกาศฟังก์ชั่นชื่อ `main` นั้นไม่มี parameters และไม่ return ค่าอะไรเลย
หากมี parameters มันจะอยู่ในวงเล็บ `()`

ภายในของฟังก์ชั่นถูกครอบด้วย `{}` โดย Rust จำเป็นต้องมีวงเล็บปีกกาครอบภายในฟังก์ชั่นทั้งหมด
เพื่อรูปแบบการเขียนที่ดี คุณควรวางวงเล็บปีกกาเปิดไว้ในบรรทัดเดียวกับการประกาศฟังก์ชั่น
โดยเพิ่มช่องว่างคั่นกลางหนึ่งช่อง

> หมายเหตุ: หากคุณต้องการใช้รูปแบบการเขียนโค้ดมาตรฐานในโปรเจกต์ Rust
> คุณสามารถใช้เครื่องมือจัดรูปแบบอัตโนมัติที่ชื่อ `rustfmt` 
> เพื่อจัดระเบียบโค้ดของคุณให้อยู่ในรูปแบบมาตรฐาน (ดูรายละเอียดเพิ่มเติมเกี่ยวกับ `rustfmt` ใน 
> [ภาคผนวก D][devtools])
> ทีมงานของ Rust ได้รวบรวมเครื่องมือไว้กับการแจกจ่าย Rust แบบมาตรฐานแล้ว
> เช่นเดียวกับ `rustc` ดังนั้นมันจึงควรถูกติดตั้งในเครื่องของคุณแล้วตอนนี้

ภายในฟังก์ชั่น `main` มีโค้ดดังต่อไปนี้:

```rust
    println!("Hello, world!");
```

บรรทัดนี้การทำงานทั้งหมดของโปรแกรมเล็ก ๆ นี้ ซึ่งจะแสดงผลข้อความออกทางหน้าจอ
มีรายละเอียดสำคัญสี่อย่างที่ควรสังเกตดังนี้

อย่างแรก รูปแบบการเขียน Rust คือการเยื้องบรรทัดด้วยช่องว่างสี่ช่อง ไม่ใช่แทบ 

อย่างที่สอง `println!` คือ macro ของ Rust โดยหากต้องการเรียกใช้ฟักง์ชั่นแทน
จำเป็นจะต้องเขียนแบบนี้ `println` (ไม่มี `!`) 
เราจะกล่าวถึงรายละเอียดเพิ่มเติมเกี่ยวกับ macro บน Rust ในบทที่ 20
สำหรับตอนนี้ คุณเพียงต้องรู้ว่าการใช้ `!` หมายถึงคุณกำลังเรียกใช้ macro 
แทนที่จะเป็นฟังก์ชั่นปกติ และ macro นั้นไม่ได้มีกฎการใช้งานเหมือนกับฟังก์ชั่นเสมอไป 

อย่างที่สาม คุณจะสังเกตเห็นข้อความ `"Hello, world!"` 
ซึ่งเราส่งข้อความนี้เป็น argument ไปยัง `println!` 
จากนั้นข้อความจะแสดงผลออกที่หน้าจอ

อย่างที่สี่ เราปิดท้ายบรรทัดด้วยเครื่องหมายอัฒภาค (`;`) 
ซึ่งระบุว่านิพจน์นี้จบการทำงานแล้ว และนิพจน์ถัดไปพร้อมจะเริ่มทำงาน
โค้ดส่วนใหญ่ของ Rust จะลงท้ายด้วยเครื่องหมายอัฒภาค

### Compiling and Running Are Separate Steps

You’ve just run a newly created program, so let’s examine each step in the
process.

Before running a Rust program, you must compile it using the Rust compiler by
entering the `rustc` command and passing it the name of your source file, like
this:

```console
$ rustc main.rs
```

If you have a C or C++ background, you’ll notice that this is similar to `gcc`
or `clang`. After compiling successfully, Rust outputs a binary executable.

On Linux, macOS, and PowerShell on Windows, you can see the executable by
entering the `ls` command in your shell:

```console
$ ls
main  main.rs
```

On Linux and macOS, you’ll see two files. With PowerShell on Windows, you’ll
see the same three files that you would see using CMD. With CMD on Windows, you
would enter the following:

```cmd
> dir /B %= the /B option says to only show the file names =%
main.exe
main.pdb
main.rs
```

This shows the source code file with the *.rs* extension, the executable file
(*main.exe* on Windows, but *main* on all other platforms), and, when using
Windows, a file containing debugging information with the *.pdb* extension.
From here, you run the *main* or *main.exe* file, like this:

```console
$ ./main # or .\main.exe on Windows
```

If your *main.rs* is your “Hello, world!” program, this line prints `Hello,
world!` to your terminal.

If you’re more familiar with a dynamic language, such as Ruby, Python, or
JavaScript, you might not be used to compiling and running a program as
separate steps. Rust is an *ahead-of-time compiled* language, meaning you can
compile a program and give the executable to someone else, and they can run it
even without having Rust installed. If you give someone a *.rb*, *.py*, or
*.js* file, they need to have a Ruby, Python, or JavaScript implementation
installed (respectively). But in those languages, you only need one command to
compile and run your program. Everything is a trade-off in language design.

Just compiling with `rustc` is fine for simple programs, but as your project
grows, you’ll want to manage all the options and make it easy to share your
code. Next, we’ll introduce you to the Cargo tool, which will help you write
real-world Rust programs.

[troubleshooting]: ch01-01-installation.html#การแกไขปัญหา
[devtools]: appendix-04-useful-development-tools.html
