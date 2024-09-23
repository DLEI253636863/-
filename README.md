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
การแก้ไขข้อบกพร่อง WordPress
ก่อนหน้า: การแก้ไขข้อบกพร่อง WordPress
ต่อไป
การดีบักเครือข่าย WordPress
ถัดไป: การดีบักเครือข่าย WordPress
บทต่างๆ
รายชื่อบท
เกี่ยวกับ
ข่าว
การโฮสติ้ง
ความเป็นส่วนตัว
ตู้โชว์
ธีม
ปลั๊กอิน
ลวดลาย
เรียนรู้
เอกสารประกอบ
นักพัฒนา
เวิร์ดเพรส.ทีวี↗
มีส่วนร่วม
กิจกรรม
บริจาค↗
ห้าเพื่ออนาคต
เวิร์ดเพรสดอทคอม↗
แมตต์↗
bbPress ↗
บัดดี้เพรส↗
เยี่ยมชมเพจ Facebook ของเรา
เยี่ยมชมบัญชี X (เดิมคือ Twitter) ของเรา
เยี่ยมชมบัญชี Instagram ของเรา
เยี่ยมชมบัญชี LinkedIn ของเรา
เยี่ยมชมช่อง YouTube ของเรา
โค้ดเป็นบทกวี
