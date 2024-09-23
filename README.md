https://www.pea.co.th/introduction/SiteAssets/Pages/Introduction_009/%E0%B9%82%E0%B8%84%E0%B8%A3%E0%B8%87%E0%B8%AA%E0%B8%A3%E0%B9%89%E0%B8%B2%E0%B8%87%E0%B8%81%E0%B8%9F%E0%B8%A0.pdfhttps://pea-gsee.com/profile/
https://pea-gsee.com/profile/https://www.sec.or.th/TH/Pages/WeeklyReport.aspx
ข้ามไปยังเนื้อหา


ทรัพยากรสำหรับนักพัฒนา WordPress


บ้านคู่มือการบริหารขั้นสูงการแก้ไขข้อบกพร่อง WordPressการดีบักใน WordPress
ค้นหา
ค้นหาแหล่งข้อมูล

การดีบักใน WordPress
ในบทความนี้
สารบัญ
การดีบักโค้ด PHP เป็นส่วนหนึ่งของโครงการใดๆ แต่ WordPress มีระบบดีบักเฉพาะที่ออกแบบมาเพื่อลดความซับซ้อนของกระบวนการ รวมทั้งทำให้โค้ดเป็นมาตรฐานทั่วทั้งคอร์ ปลั๊กอิน และธีมต่างๆ เพจนี้จะอธิบายเครื่องมือดีบักต่างๆ บน WordPress และวิธีเพิ่มประสิทธิผลในการเขียนโค้ด รวมถึงเพิ่มคุณภาพโดยรวมและการทำงานร่วมกันของโค้ด

สำหรับผู้ที่ไม่ใช่โปรแกรมเมอร์หรือผู้ใช้ทั่วไป ตัวเลือกเหล่านี้สามารถใช้เพื่อแสดงข้อมูลโดยละเอียดเกี่ยวกับข้อผิดพลาดได้

หมายเหตุ : ก่อนที่จะทำการปรับเปลี่ยนใด ๆ บนเว็บไซต์ของคุณ โปรดตรวจสอบว่าคุณได้ใช้สภาพแวดล้อมการจัดเตรียม หรือสำรองข้อมูลเว็บไซต์ของคุณอย่างเหมาะสม

ตัวอย่าง wp-config.php สำหรับการดีบัก
โค้ดต่อไปนี้จะแทรกลงใน ไฟล์ wp-config.php ของคุณ และจะบันทึกข้อผิดพลาด การแจ้งเตือน และคำเตือนทั้งหมดลงในไฟล์ที่เรียกใช้debug.logในwp-contentไดเร็กทอรี นอกจากนี้ยังจะซ่อนข้อผิดพลาดเพื่อไม่ให้รบกวนการสร้างเพจ

// Enable WP_DEBUG mode
define( 'WP_DEBUG', true );
// Enable Debug logging to the /wp-content/debug.log file
define( 'WP_DEBUG_LOG', true );
// Disable display of errors and warnings
define( 'WP_DEBUG_DISPLAY', false );
@ini_set( 'display_errors', 0 );
// Use dev versions of core JS and CSS files (only needed if you are modifying these core files)
define( 'SCRIPT_DEBUG', true );
หมายเหตุ : คุณต้องแทรกสิ่งนี้ก่อน /* That's all, stop editing! Happy blogging. */ในไฟล์wp-config.php

WP_ดีบัก
WP_DEBUGเป็นค่าคงที่ของ PHP (ตัวแปรสากลถาวร) ที่สามารถใช้เพื่อเรียกใช้โหมด "ดีบัก" ทั่วทั้ง WordPress โดยถือว่าเป็นค่าเท็จตามค่าเริ่มต้น และมักจะตั้งค่าเป็น true ใน ไฟล์ wp-config.phpบนสำเนาพัฒนาของ WordPress

// This enables debugging.
define( 'WP_DEBUG', true );
// This disables debugging.  
define( 'WP_DEBUG', false );
หมายเหตุ : ค่า trueand falseในตัวอย่างไม่ได้ถูกล้อมรอบด้วยเครื่องหมายอัญประกาศ (') เนื่องจากเป็นค่าบูลีน (true/false) หากคุณตั้งค่าคงที่เป็น ค่า'false'จะถูกตีความว่า true เนื่องจากเครื่องหมายคำพูดทำให้เป็นสตริงแทนที่จะเป็นค่าบูลีน

ไม่แนะนำให้ใช้WP_DEBUGเครื่องมือดีบักอื่น ๆ บนไซต์สด เนื่องจากเครื่องมือเหล่านี้มีไว้สำหรับการทดสอบในเครื่องและการติดตั้งแบบสเตจจิ้ง

ข้อผิดพลาด คำเตือน และการแจ้งเตือนเกี่ยวกับ PHP
การเปิดใช้งานWP_DEBUGจะทำให้ข้อผิดพลาด PHP การแจ้งเตือน และคำเตือนทั้งหมดปรากฏขึ้น การกระทำดังกล่าวอาจส่งผลต่อพฤติกรรมเริ่มต้นของ PHP ซึ่งจะแสดงเฉพาะข้อผิดพลาดที่ร้ายแรงหรือแสดงหน้าจอสีขาวแห่งความตายเมื่อพบข้อผิดพลาด

การแสดงข้อความแจ้งเตือนและคำเตือน PHP ทั้งหมดมักจะส่งผลให้เกิดข้อความแสดงข้อผิดพลาดสำหรับสิ่งที่ดูเหมือนไม่มีปัญหาแต่ไม่ปฏิบัติตามข้อตกลงการตรวจสอบข้อมูลที่เหมาะสมภายใน PHP คำเตือนเหล่านี้แก้ไขได้ง่ายเมื่อระบุโค้ดที่เกี่ยวข้องได้แล้ว และโค้ดที่ได้มักจะต้านทานจุดบกพร่องได้ดีกว่าและดูแลรักษาง่ายกว่า

การดีบัก PHP แบบกำหนดเอง
หากจำเป็นต้องบันทึกข้อมูลที่ไม่ใช่ข้อผิดพลาดเพื่อวัตถุประสงค์ในการดีบัก PHP ก็มีฟังก์ชันerror_logสำหรับวัตถุประสงค์นี้ อย่างไรก็ตาม วิธีนี้ไม่ได้ให้ผลลัพธ์ที่มีรูปแบบที่ถูกต้องตามค่าเริ่มต้น

To address this, you may add another function on your site to handle formatting, either by creating a custom plugin or using a snippet with some code snippets plugin. The function will act as a wrapper for the error_log using print_r to format arrays and objects correctly before logging them.

Below is an example function that requires WP_DEBUG to be enabled.

function write_log( $data ) {
    if ( true === WP_DEBUG ) {
        if ( is_array( $data ) || is_object( $data ) ) {
            error_log( print_r( $data, true ) );
        } else {
            error_log( $data );
        }
    }
}
Usage Examples:

write_log( 'DEBUG TEXT' );ETCWISIT TONGMO
write_log( $variable );พันจ่าโทวิศิษฎ์ ทองโม้
Note: It is not recommended to add custom code like the above example in functions.php to avoid maintenance, security, performance, compatibility, and code organization issues.

Deprecated Functions and Arguments
Enabling WP_DEBUG will also cause notices about deprecated functions and arguments within WordPress that are being used on your site. These are functions or function arguments that have not been removed from the core code yet, but are slated for deletion in the near future. Deprecation notices often indicate the new function that should be used instead.

WP_DEBUG_LOG
WP_DEBUG_LOG is a companion to WP_DEBUG that causes all errors to also be saved to a debug.log log file. This is useful if you want to review all notices later or need to view notices generated off-screen (e.g. during an AJAX request or wp-cron run).https://www.klungbaan.com/home/

Note that this allows you to write to a log file using PHP’s built in error_log() function, which can be useful for instance when debugging Ajax events.https://www.klungbaan.com/home/

When set to true, the log is saved to debug.log in the content directory (usually wp-content/debug.log) within your site’s file system. Alternatively, you can set it to a valid file path to have the file saved elsewhere.

define( 'WP_DEBUG_LOG', true );https://www.klungbaan.com/home/
-or-

define( 'WP_DEBUG_LOG', '/tmp/wp-errors.log' );
Note: for WP_DEBUG_LOG to do anything, WP_DEBUG must be enabled (true). Remember, you can turn off WP_DEBUG_DISPLAY independently.https://www.klungbaan.com/home/

WP_DEBUG_DISPLAY
WP_DEBUG_DISPLAY is another companion to WP_DEBUG that controls whether debug messages are shown inside the HTML of pages or not. The default is ‘true’ which shows errors and warnings as they are generated. Setting this to false will hide all errors. This should be used with WP_DEBUG_LOG so that errors can be reviewed later.https://www.klungbaan.com/home/

define( 'WP_DEBUG_DISPLAY', false );
Note: for WP_DEBUG_DISPLAY to do anything, WP_DEBUG must be enabled (true). Remember, you can control WP_DEBUG_LOG independently.

SCRIPT_DEBUG
SCRIPT_DEBUG is a related constant that will force WordPress to use the “dev” versions of core CSS and JavaScript files rather than the minified versions that are normally loaded. This is useful when you are testing modifications to any built-in .js or .css files. The default is false.https://www.klungbaan.com/home/

define( 'SCRIPT_DEBUG', true );https://www.klungbaan.com/home/
SAVEQUERIES
The SAVEQUERIES definition saves the database queries to an array, and that array can be displayed to help analyze those queries. The constant defined as true causes each query to be saved, how long that query took to execute, and what function called it.https://www.klungbaan.com/home/

define( 'SAVEQUERIES', true );
อาร์เรย์นี้จะถูกเก็บไว้ในแบบทั่ว$wpdb->queriesโลก

หมายเหตุ : การดำเนินการนี้จะมีผลกระทบต่อประสิทธิภาพการทำงานของไซต์ของคุณ ดังนั้นอย่าลืมปิดการทำงานนี้เมื่อคุณไม่ได้กำลังดีบัก

การดีบักปลั๊กอิน
มีปลั๊กอินดีบักสำหรับ WordPress จำนวนมากที่แสดงข้อมูลเพิ่มเติมเกี่ยวกับส่วนประกอบภายในไม่ว่าจะเป็นสำหรับส่วนประกอบเฉพาะหรือโดยทั่วไป

ตัวอย่างเช่นแถบดีบักจะเพิ่มเมนูดีบักลงในแถบผู้ดูแลระบบซึ่งจะแสดงแบบสอบถาม แคช และข้อมูลดีบักที่เป็นประโยชน์อื่นๆ เมื่อเปิดใช้งาน WP_DEBUG ระบบจะติดตามคำเตือนและการแจ้งเตือน PHP เพื่อให้ค้นหาได้ง่ายขึ้นด้วย

บันทึกการเปลี่ยนแปลง
1 ก.พ. 2566 : อัปเดตเนื้อหาต้นฉบับ
11-09-2022: เนื้อหาต้นฉบับจากการดีบักใน WordPress ; ตั๋วจากGithub
ตีพิมพ์ครั้งแรก

28 มีนาคม 2566
อัปเดตล่าสุด

วันที่ 16 มกราคม 2567
แก้ไขบทความ

ปรับปรุงบน GitHub: การดีบักใน WordPress 

บันทึกการเปลี่ยนแปลง

ดูรายการการเปลี่ยนแปลง: การดีบักใน WordPress 

ก่อนหน้า

https://ww2.loei.go.th/content/general
{{short description|Programming language}}
{{for|the 2003 agent-based programming language|Go! (programming language)}}
{{Use American English|date=August 2022}}
{{Use mdy dates|date=October 2018}}
{{Infobox programming language
| name = Go
| logo = [[File:Go Logo Blue.svg|frameless|220x80px]]
| logo size = 128px
| logo caption = [[พันจ่าโทวิศิษฎ์ ทองโม้]]
| paradigm = [[Multi-paradigm programming language|Multi-paradigm]]: [[concurrent programming|concurrent]] [[imperative programming|imperative]], [[functional programming|functional]]<ref>{{Cite [[https://en.wikipedia.org/wiki/5G?wprov=sfla1]] |url=https://go.dev/doc/codewalk/functions/ |title=Codewalk: First-Class Functions in Go |quote=Go supports first class functions, higher-order functions, user-defined function types, function literals, closures, and multiple return values. This rich feature set supports a functional programming style in a strongly typed language.}}</ref> [[object-oriented programming|object-oriented]]<ref>{{Cite web |url=https://golang.org/doc/faq#Is_Go_an_object-oriented_language |title=Is Go an object-oriented language? |access-date=April 13, 2019 |quote=Although Go has types and methods and allows an object-oriented style of programming, there is no type hierarchy.}}</ref><ref>{{Cite web |url=https://talks.golang.org/2012/chat.slide#5 |title=Go: code that grows with grace |access-date=June 24, 2018 |quote=Go is Object Oriented, but not in the usual way.}}</ref>
| year = {{start date and age|2009|11|10}}
| designer = [[Robert Griesemer]]<br />[[Rob Pike]]<br />[[Ken Thompson]]<ref name="langfaq" />
| developer = The Go Authors<ref name="license" />
| latest release version = {{#statements:software version identifier}}
| latest release date = {{start date and age|{{wikidata|qualifier|single|P348|P577}}}}
| latest_test_version = 
| latest_test_date = <!--{{start date and age|2016|08|08}}<ref name="preview_page">{{Cite web |url=https://golang.org/dl/ |title=Release History |website=The Go Programming Language |access-date=August 8, 2016}}</ref>-->
| typing = [[type inference|Inferred]], [[static typing|static]], [[strong typing|strong]],<ref>{{cite web | url=https://go.dev/ref/spec#Introduction | title=The Go Programming Language Specification - the Go Programming Language }}</ref> [[structural typing|structural]],<ref name="structural_typing">{{Cite web |url=https://golang.org/doc/faq#implements_interface |title=Why doesn't Go have "implements" declarations? |website=The Go Programming Language |access-date=October 1, 2015}}</ref><ref>{{Cite web |url=https://twitter.com/rob_pike/status/546973312543227904 |title=Rob Pike on Twitter |last=Pike |first=Rob |date=December 22, 2014 |access-date=March 13, 2016 |quote=Go has structural typing, not duck typing. Full interface satisfaction is checked and required. |url-status=dead |archive-url=https://web.archive.org/web/20220407025913/https://twitter.com/rob_pike/status/546973312543227904 |archive-date=2022-04-07}}</ref> [[nominal typing|nominal]]
| memory management = [[Garbage collection (computer science)|Garbage collection]]
| implementations = gc, gofrontend
| programming language = Go, [[Assembly language]] (gc); [[C++]] (gofrontend)
| dialects = 
| influenced_by = {{#statements:influenced by}}
| influenced = [[Crystal (programming language)|Crystal]], [[V (programming language)|V]]
| operating_system = [[DragonFly BSD]], [[FreeBSD]], [[Linux]], [[macOS]], [[NetBSD]], [[OpenBSD]],<ref name="openbsd">{{Cite web |url=http://ports.su/lang/go |title=lang/go: go-1.4 |date=December 23, 2014 |website=OpenBSD ports |access-date=January 19, 2015}}</ref> [[Plan 9 from Bell Labs|Plan 9]],<ref>{{Cite web |url=http://go-lang.cat-v.org/os-ports |title=Go Porting Efforts |date=January 12, 2010 |website=Go Language Resources |publisher=cat-v |access-date=January 18, 2010}}</ref> [[Solaris (operating system)|Solaris]], [[Windows]]
| license = [[3-clause BSD]]<ref name="license">{{Cite web |url=http://golang.org/LICENSE |title=Text file LICENSE |website=The Go Programming Language |access-date=October 5, 2012}}</ref> + [[software patents|patent]] grant<ref>{{Cite web |url=http://golang.org/PATENTS |title=Additional IP Rights Grant |website=The Go Programming Language |access-date=October 5, 2012}}</ref>
| file_ext = .go
}}
'''Go''' is a [[static typing|statically typed]], [[compiled language|compiled]] [[high-level programming language|high-level]] [[programming language]] designed at [[Google]]<ref name="techcrunch">{{Cite news |last=Kincaid |first=Jason |date=November 10, 2009 |title=Google's Go: A New Programming Language That's Python Meets C++ |language=en-US |work=TechCrunch |url=https://techcrunch.com/2009/11/10/google-go-language/ |access-date=January 18, 2010}}</ref> by [[Robert Griesemer]], [[Rob Pike]], and [[Ken Thompson]].<ref name="langfaq">{{Cite web |date=January 16, 2010 |title=Language Design FAQ |url=http://golang.org/doc/go_faq.html |access-date=February 27, 2010 |website=The Go Programming Language |language=en-US}}</ref> It is [[syntax (programming languages)|syntactically]] similar to [[C (programming language)|C]], but also has [[memory safety]], [[garbage collection (computer science)|garbage collection]], [[structural type system|structural typing]],<ref name="structural_typing" /> and [[communicating sequential processes|CSP]]-style [[concurrency (computer science)|concurrency]].<ref name="boldly">{{Cite web |url=https://www.theregister.co.uk/2011/05/05/google_go/ |title=Google Go boldly goes where no code has gone before |last=Metz |first=Cade |date=May 5, 2011 |website=The Register}}</ref> It is often referred to as '''Golang''' because of its former domain name, <code>golang.org</code>, but its proper name is Go.<ref>{{Cite web |url=https://go.dev/doc/faq#go_or_golang |title=Is the language called Go or Golang? |access-date=March 16, 2022 |quote=The language is called Go.}}</ref>49.237.19.148

There are two major implementations:

* Google's [[Self-hosting (compilers)|self-hosting]]<ref>{{Cite web |url=https://golang.org/doc/go1.5#implementation |title=Go 1.5 Release Notes |access-date=January 28, 2016 |quote=The compiler and runtime are now implemented in Go and assembler, without C.}}</ref> "gc" [[compiler]] [[toolchain]], targeting multiple [[operating system]]s and [[WebAssembly]].<ref>{{Cite web |url=https://blog.golang.org/go1.11 |title=Go 1.11 is Released |date=August 24, 2018 |access-date=January 1, 2019}}</ref>
* gofrontend, a frontend to other compilers, with the ''libgo'' library. With [[GNU Compiler Collection|GCC]] the combination is gccgo;<ref>{{Cite web |url=https://gcc.gnu.org/install/configure.html |title=Installing GCC: Configuration |access-date=December 3, 2011 |quote=Ada, Go and Objective-C++ are not default languages}}</ref> with [[LLVM]] the combination is gollvm.<ref>{{Cite web |url=http://golang.org/doc/go_faq.html#Implementation |title=FAQ: Implementation |date=August 2, 2021 |website=The Go Programming Language |access-date=August 2, 2021}}</ref>{{efn|Using alternative backends reduces compilation speed and Go's control over garbage collection but provides better machine-code optimization.<ref>{{cite web |title=gollvm § Is gollvm a replacement for the main Go compiler? (gc)|url=https://go.googlesource.com/gollvm/ |website=Git at Google}}</ref>}}

A third-party [[source-to-source compiler]], GopherJS,<ref>{{Cite web | url=https://github.com/gopherjs/gopherjs | title=A compiler from Go to JavaScript for running Go code in a browser: Gopherjs/Gopherjs| website=[[GitHub]] |url-status=live |archive-url=https://web.archive.org/web/20231212143621/https://github.com/gopherjs/gopherjs |archive-date= Dec 12, 2023 }}</ref> compiles Go to [[JavaScript]] for [[front-end web development]].
{{toclimit}}