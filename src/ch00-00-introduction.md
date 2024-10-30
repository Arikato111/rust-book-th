#  บทนำ

> หมายเหตุ: หนังสือฉบับนี้เป็นฉบับเดียวกับ [The Rust Programming
> Language][nsprust] ซึ่งมีจำหน่ายทั้งในรูปแบบหนังสือและอีบุ๊กที่ 
> [No Starch Press][nsp]

[nsprust]: https://nostarch.com/rust-programming-language-2nd-edition
[nsp]: https://nostarch.com/

ยินดีต้อนรับสู่ *ภาษาโปรแกรม Rust* หนังสือแนะนำเกี่ยวกับ Rust
ภาษาโปรแกรม Rust ช่วยให้คุณเขียนซอฟต์แวร์ได้อย่างรวดเร็วและเชื่อถือได้
การยศาสตร์ระดับสูงและการควบคุมระดับต่ำ มักจะขัดแย้งกันในการออกแบบภาษาโปรแกรม
Rust กำลังท้าทายความขัดแย้งดังกล่าว ด้วยการสร้างสมดุลระหว่างความสามารถทางเทคนิคอังทรงพลัง
และประสบการณ์ของนักพัฒนาที่ยอดเยี่ยม
Rust ให้ทางเลือกับคุณในการควบคุมรายละเอียดระดับต่ำ (เช่นการใช้หน่วยความจำ) 
โดยปราศจากความยุ่งยากที่เกี่ยวข้องกับการควบคุมดังกล่าว

## Rust เหมาะกับใคร

Rust เหมาะกับหลาย ๆ คน ด้วยเหตุผลหลากหลายประการ ลองดูบางกลุ่มจากกลุ่มคนที่สำคัญที่สุดกัน

### ทีมงานนักพัฒนา

Rust ได้พิสูจน์แล้วว่าเป็นเครื่องมือที่มีประสิทธิภาพ
ในการทำงานร่วมกันระหว่างทีมนักพัฒนาขนาดใหญ่ 
ที่มีความรู้ด้านการเขียนโปรแกรมระบบในระดับต่าง ๆ 
โค้ดระดับต่ำมีแนวโน้มที่จะเกิดข้อบกพร่องเล็ก ๆ น้อย ๆ มากมาย 
ซึ่งในภาษาอื่น ๆ ส่วนใหญ่สามารถตรวจพบได้โดยการทดสอบอย่างละเอียด 
โดยนักพัฒนาที่มีประสบการณ์เท่านั้น
ใน Rust คอมไพเลอร์มีบทบาทเป็นผู้เฝ้าประตู โดยปฏิเสธที่จะคอมไพล์โค้ดที่มีข้อบกพร่องที่เข้าใจอยากเหล่านี้
รวมถึงข้อบกพร่องที่เกิดขึ้นพร้อมกัน ด้วยการทำงานร่วมกับคอมไพเลอร์ ทีมต่าง ๆ จึงสามารถใช้เวลามุ่งเน้นไปที่ตรรกะของโปรแกรม แทนที่จะไล่ตามจุดบกพร่อง

Rust ยังนำเครื่องมือการพัฒนาที่ทันสมัยมาสู่โลกแห่งการเขียนโปรแกรมระบบ

* Cargo คือเครื่องมือจัดการการพึ่งพา (dependency) และการคอมไพล์แบบบูรณาการ
ทำให้การเพิ่ม การคอมไพล์ และการจัดการการพึ่งพา นั้นง่ายดายและสอดคล้องกันทั่วทั้งระบบนิเวศของ Rust
* Rustfmt เครื่องมือจัดรูปแบบโค้ด ที่ช่วยให้นักพัฒนาซอฟต์แวร์มีรูปแบบการเขียนโค้ดที่สอดคล้องกัน
* rust-analyzer รองรับการเติมโค้ดให้สมบูรณ์ และข้อความแสดงข้อผิดพลาดในบรรทัด 
ผ่านการทำงานร่วมกับสภาพแวดล้อมสำหรับการพัฒนาแบบเบ็ดเสร็จ (IDE)

การใช้เครื่องมือเหล่านี้และเครื่องมืออื่น ๆ ในระบบนิเวศของ Rust 
ช่วยให้นักพัฒนาทำงานได้อย่างมีประสิทธิภาพ
ขณะเขียนโค้ดระดับระบบ (systems-level code)

### นักเรียน

Rust เหมาะกับนักเรียน และผู้ที่สนใจในการเรียนรู้เกี่ยวกับแนวคิดของระบบ
ในการใช้งาน Rust ผู้คนต่าง ๆ จะได้เรียนรู้เกี่ยวกับหัวข้อต่าง ๆ เช่น การพัฒนาระบบปฏิบัติการ
ชุมชนมีความยินดีเป็นอย่างยิ่ง และยินดีที่จะตอบคำถามของนักเรียน
ด้วยความพยายามเช่นหนังสือเล่มนี้ ทีมงาน Rust 
หวังว่าจะทำให้ผู้คนจำนวนมากสามารถเข้าถึงแนวคิดของระบบได้
โดยเฉพาะผู้ที่กำลังเริ่มเขียนโปรแกรม

### บริษัท

บริษัทหลายร้อยแห่ง ทั้งขนาดใหญ่และขนาดเล็ก ต่างใช้ Rust ในการพัฒนาสำหรับงานที่หลากหลาย
ไม่ว่าจะเป็น โปรแกรมบรรทัดคำสั่ง, บริการเว็บ, เครื่องมือ DevOps, อุปกรณ์ฝังตัว, 
การวิเคราะห์และการแปลงรหัสเสียงและวิดีโอ, คริปโทเคอร์เรนซี, ชีวสารสนเทศศาสตร์, เครื่องมือค้นหา, 
แอปพลิเคชั่นอินเทอร์เน็ตของสรรพสิ่ง, การเรียนรู้ของเครื่อง (machine learning)
และแม้แต่ส่วนสำคัญของเบราว์เซอร์ Firefox

### Open Source Developers

Rust is for people who want to build the Rust programming language, community,
developer tools, and libraries. We’d love to have you contribute to the Rust
language.

### People Who Value Speed and Stability

Rust is for people who crave speed and stability in a language. By speed, we
mean both how quickly Rust code can run and the speed at which Rust lets you
write programs. The Rust compiler’s checks ensure stability through feature
additions and refactoring. This is in contrast to the brittle legacy code in
languages without these checks, which developers are often afraid to modify. By
striving for zero-cost abstractions, higher-level features that compile to
lower-level code as fast as code written manually, Rust endeavors to make safe
code be fast code as well.

The Rust language hopes to support many other users as well; those mentioned
here are merely some of the biggest stakeholders. Overall, Rust’s greatest
ambition is to eliminate the trade-offs that programmers have accepted for
decades by providing safety *and* productivity, speed *and* ergonomics. Give
Rust a try and see if its choices work for you.

## Who This Book Is For

This book assumes that you’ve written code in another programming language but
doesn’t make any assumptions about which one. We’ve tried to make the material
broadly accessible to those from a wide variety of programming backgrounds. We
don’t spend a lot of time talking about what programming *is* or how to think
about it. If you’re entirely new to programming, you would be better served by
reading a book that specifically provides an introduction to programming.

## How to Use This Book

In general, this book assumes that you’re reading it in sequence from front to
back. Later chapters build on concepts in earlier chapters, and earlier
chapters might not delve into details on a particular topic but will revisit
the topic in a later chapter.

You’ll find two kinds of chapters in this book: concept chapters and project
chapters. In concept chapters, you’ll learn about an aspect of Rust. In project
chapters, we’ll build small programs together, applying what you’ve learned so
far. Chapters 2, 12, and 20 are project chapters; the rest are concept chapters.

Chapter 1 explains how to install Rust, how to write a “Hello, world!” program,
and how to use Cargo, Rust’s package manager and build tool. Chapter 2 is a
hands-on introduction to writing a program in Rust, having you build up a
number guessing game. Here we cover concepts at a high level, and later
chapters will provide additional detail. If you want to get your hands dirty
right away, Chapter 2 is the place for that. Chapter 3 covers Rust features
that are similar to those of other programming languages, and in Chapter 4
you’ll learn about Rust’s ownership system. If you’re a particularly meticulous
learner who prefers to learn every detail before moving on to the next, you
might want to skip Chapter 2 and go straight to Chapter 3, returning to Chapter
2 when you’d like to work on a project applying the details you’ve learned.

Chapter 5 discusses structs and methods, and Chapter 6 covers enums, `match`
expressions, and the `if let` control flow construct. You’ll use structs and
enums to make custom types in Rust.

In Chapter 7, you’ll learn about Rust’s module system and about privacy rules
for organizing your code and its public Application Programming Interface
(API). Chapter 8 discusses some common collection data structures that the
standard library provides, such as vectors, strings, and hash maps. Chapter 9
explores Rust’s error-handling philosophy and techniques.

Chapter 10 digs into generics, traits, and lifetimes, which give you the power
to define code that applies to multiple types. Chapter 11 is all about testing,
which even with Rust’s safety guarantees is necessary to ensure your program’s
logic is correct. In Chapter 12, we’ll build our own implementation of a subset
of functionality from the `grep` command line tool that searches for text
within files. For this, we’ll use many of the concepts we discussed in the
previous chapters.

Chapter 13 explores closures and iterators: features of Rust that come from
functional programming languages. In Chapter 14, we’ll examine Cargo in more
depth and talk about best practices for sharing your libraries with others.
Chapter 15 discusses smart pointers that the standard library provides and the
traits that enable their functionality.

In Chapter 16, we’ll walk through different models of concurrent programming and
talk about how Rust helps you to program in multiple threads fearlessly. In
Chapter 17, we will build on that by exploring Rust’s async and await syntax and
the lightweight concurrency model they support.

Chapter 18 looks at how Rust idioms compare to object-oriented programming
principles you might be familiar with.

Chapter 19 is a reference on patterns and pattern matching, which are powerful
ways of expressing ideas throughout Rust programs. Chapter 20 contains a
smorgasbord of advanced topics of interest, including unsafe Rust, macros, and
more about lifetimes, traits, types, functions, and closures.

In Chapter 21, we’ll complete a project in which we’ll implement a low-level
multithreaded web server!

Finally, some appendices contain useful information about the language in a
more reference-like format. Appendix A covers Rust’s keywords, Appendix B
covers Rust’s operators and symbols, Appendix C covers derivable traits
provided by the standard library, Appendix D covers some useful development
tools, and Appendix E explains Rust editions. In Appendix F, you can find
translations of the book, and in Appendix G we’ll cover how Rust is made and
what nightly Rust is.

There is no wrong way to read this book: if you want to skip ahead, go for it!
You might have to jump back to earlier chapters if you experience any
confusion. But do whatever works for you.

<span id="ferris"></span>

An important part of the process of learning Rust is learning how to read the
error messages the compiler displays: these will guide you toward working code.
As such, we’ll provide many examples that don’t compile along with the error
message the compiler will show you in each situation. Know that if you enter
and run a random example, it may not compile! Make sure you read the
surrounding text to see whether the example you’re trying to run is meant to
error. Ferris will also help you distinguish code that isn’t meant to work:

| Ferris                                                                                                           | Meaning                                          |
|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| <img src="img/ferris/does_not_compile.svg" class="ferris-explain" alt="Ferris with a question mark"/>            | This code does not compile!                      |
| <img src="img/ferris/panics.svg" class="ferris-explain" alt="Ferris throwing up their hands"/>                   | This code panics!                                |
| <img src="img/ferris/not_desired_behavior.svg" class="ferris-explain" alt="Ferris with one claw up, shrugging"/> | This code does not produce the desired behavior. |

In most situations, we’ll lead you to the correct version of any code that
doesn’t compile.

## Source Code

The source files from which this book is generated can be found on
[GitHub][book].

[book]: https://github.com/rust-lang/book/tree/main/src
