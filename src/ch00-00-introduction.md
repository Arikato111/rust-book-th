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
แอปพลิเคชั่นอินเทอร์เน็ตของสรรพสิ่ง (IOT), การเรียนรู้ของเครื่อง (machine learning)
และแม้แต่ส่วนสำคัญของเบราว์เซอร์ Firefox

### นักพัฒนาโอเพนซอร์ส

Rust เหมาะกับผู้ที่ต้องการพัฒนาภาษาโปรแกรม Rust, ชุมชน, เครื่องมือสำหรับนักพัฒนา,
และไลบรารีของ Rust  เราหวังอย่างยิ่งว่าคุณจะมีส่วนร่วมในภาษา Rust

### ผู้ที่ให้ความสำคัญกับความเร็วและความเสถียร

Rust เหมาะสำหรับผู้ที่ต้องการความเร็วและความเสถียรของภาษาโปรแกรม 
ความเร็วในที่นี้หมายถึง ความเร็วของโปรแกรมที่สร้างจาก Rust และความเร็วในการเขียนโปรแกรมของคุณ
การตรวจสอบของคอมไพเลอร์ Rust จะทำให้คุณมั่นใจได้ในความเสถียร ผ่านการเพิ่มฟีเจอร์และการปรับโครงสร้างใหม่
สิ่งนี้ตรงกันข้ามกับโค้ดดั้งเดิมอันเปราะบาง ในภาษาที่ไม่มีการตรวจสอบ ซึ่งนักพัฒนามักกลัวที่จะแก้ไข
ด้วยการมุ่งเน้นไปที่ zero-cost abstractions 
ฟีเจอร์ระดับสูงสามารถคอมไพล์เป็นโค้ดระดับต่ำ ที่มีประสิทธิภาพเท่ากับโค้ดที่เขียนด้วยมือ
Rust มีความมุ่งมั่นที่จะสร้างโค้ดที่ปลอดภัยและรวดเร็วควบคู่กัน

ภาษา Rust หวังที่จะสนับสนุนผู้ใช้งานรายอื่นเช่นกัน ที่ได้กล่าวถึงข้างต้นนั้นเป็นเพียงผู้ที่มีส่วนได้ส่วนเสียรายใหญ่ที่สุดบางส่วนเท่านั้น
โดยรวมแล้ว เป้าหมายที่ยิ่งใหญ่ที่สุดของ Rust คือการกำจัดข้อเสียที่โปรแกรมเมอร์ยอมรับมานานหลายทศวรรษ
ด้วยการมอบความปลอดภัย*และ*ประสิทธิภาพการทำงาน ความเร็ว*และ*การยศาสตร์
ลองใช้ Rust ดูว่าเป็นตัวเลือกที่เหมาะกับคุณหรือไม่

## หนังสือเล่มนี้เหมาะกับใคร

หนังสือเล่มนี้คาดการณ์ว่าคุณได้เขียนโค้ดในภาษาโปรแกรมอื่นมาก่อน แต่ไม่ได้เจาะจงว่าเป็นภาษาใด 
เราได้พยายามทำให้เนื้อหานี้สามารถเข้าถึงได้จากผู้ที่มีพื้นฐานการเขียนโปรแกรมที่หลากหลาย
เราไม่ได้พูดอะไรมากมายเกี่ยวกับการเขียนโปรแกรมและวิธีคิดของมัน
หากคุณเป็นมือใหม่ในการเขียนโปรแกรม คุณควรอ่านหนังสือที่ให้พื้นฐานเกี่ยวกับการเขียนโปรแกรมโดยเฉพาะ

## วิธีใช้งานหนังสือเล่มนี้

โดยทั่วไป หนังสือเล่มนี้จะถือว่าคุณได้อ่านตามลำดับจากหน้าไปหลัง บทถัด ๆ ไปจะสร้างจากแนวคิดในบทก่อนหน้า
และบทก่อนหน้าอาจไม่เจาะลึกรายละเอียดในหัวข้อใดหัวข้อหนึ่ง แต่จะกลับมาพูดถึงหัวข้อนั้นอีกครั้งในบทต่อ ๆ ไป

คุณจะพบว่ามีบทสองประเภทในหนังสือเล่มนี้ คือบทภาคทฤษฎี และบทภาคปฏิบัติ
ในบทภาคทฤษฎี คุณจะได้เรียนรู้เกี่ยวกับแง่มุมหนึ่งของ Rust 
ในบทภาคปฏิบัติ เราจะพาคุณสร้างโปรแกรมเล็ก ๆ โดยนำสิ่งที่คุณได้เรียนรู้มาประยุกต์ใช้
บทที่ 2 12 และ 20 เป็นบทภาคปฏิบัติ ส่วนที่เหลือเป็นบทภาคทฤษฎี

บทที่ 1 จะอธิบายวิธีการติดตั้ง Rust วิธีเขียนโปรแกรม “Hello, world!” 
และวิธีใช้งาน Cargo ซึ่งเป็นเครื่องมือจัดการแพ็คเก็จและเครื่องมือคอมไพล์แบบบูรณาการ
บทที่ 2 เป็นการแนะนำการเขียนภาษา Rust แบบลงมือทำ โดยจะให้คุณสร้างเกมทายตัวเลขขึ้นมา
ใบบทถัด ๆ ไปจะครอบคลุมถึงแนวคิดระดับสูงและรายละเอียดเพิ่มเติม
หากคุณต้องการเข้าสู่โลกของ Rust ทันที่
หากคุณต้องการเริ่มเขียน Rust ทันที บทที่ 2 จะเหมาะสำหรับคุณ
บทที่ 3 ครอบคลุมถึงคุณสมบัติต่าง ๆ ของ Rust ที่คล้ายกับภาษาโปรแกรมอื่น ๆ 
และในบทที่ 4 คุณจะได้เรียนรู้เกี่ยวกับระบบ ownership ของ Rust
หากคุณเป็นผู้เรียนที่ละเอียดรอบคอบเป็นพิเศษ และชอบที่จะเรียนรู้ทุกรายละเอียดก่อนจะไปบทถัดไป
คุณอาจต้องการข้ามบทที่ 2 ไปยังบทที่ 3 เพื่อเก็บรายละเอียดต่าง ๆ ก่อนจะกลับมายังบทที่ 2 เพื่อลงมือปฏิบัติไปพร้อมกับรายละเอียดที่คุณได้รับ

บทที่ 5 จะกล่าวถึง struct และ method
และบทที่ 6 เนื้อหาจะครอบคุมถึง enum, การส่งออก `match`, 
และโครงสร้างควบคุมการทำงาน `if let`
ใน Rust คุณสามารถใช้ struct และ enum เพื่อสร้างประเภทของตัวแปรที่คุณกำหนดเองได้ (custom types)

ในบทที่ 7 คุณจะได้เรียนรู้กับระบบ module ของ Rust และกฎเกณฑ์ความเป็นส่วนตัวเพื่อจัดระเบียบโค้ดของคุณ
และส่วนต่อประสานโปรแกรมประยุกต์ (API)
บทที่ 8 จะกล่าวถึงโครงสร้างข้อมูลการรวบรวมโดยทั่วไปบางอย่าง ที่ไลบรารีมาตรฐานจัดเตรียมไว้แล้ว เช่น vector,
string, และ hash map
บทที่ 9 จะสำรวจปรัชญาและเทคนิคการจัดการข้อผิดพลาดของ Rust

บทที่ 10 จะเจาะลึกเกี่ยวกับ trait และ lifetime โดยทั่วไป ซึ่งให้อำนาจแก่คุณในการกำหนดโค้ดที่นำไปใช้กับหลากหลายประเภท
บทที่ 11 เป็นเรื่องเกี่ยวกับการทดสอบ ซึ่งแม้จะมีการรับประกันความปลอดภัยของ Rust 
แต่ก็เป็นสิ่งจำเป็นเพื่อให้แน่ใจว่าโปรแกรมของคุณทำงานได้อย่างถูกต้อง 
ในบทที่ 12 เราจะพาคุณสร้างโปรแกรมที่มีการทำงานบางอย่าง จากโปรแกรมบรรทัดคำสั่ง `grep` ซึ่งสามารถค้นหาข้อความภายในไฟล์ โดยเราจะใช้แนวคิดหลายอย่างที่ได้กล่าวถึงในบทที่แล้ว

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
