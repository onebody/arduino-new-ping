# NewPing Library for Arduino (Ultrasonic Sensors) #

**Background:**<br>
When I first received an ultrasonic sensor I was not happy with how poorly it performed. I soon realized the problem wasn't the sensor, it was the available ping and ultrasonic libraries causing the problem. The NewPing library totally fixes these problems, adds many new features, and breathes new life into these very affordable distance sensors.<br>
<br><br>

<b>Having a Conflict with the Tone Library or Timer 2?</b><br>
Instead of the tone library, use my <b><a href='https://code.google.com/p/arduino-new-tone/'>NewTone</a></b> or <b><a href='http://code.google.com/p/arduino-tone-ac'>toneAC</a></b> libraries which instead uses timer 1 (and also has many other advantages).<br>
<br><br>

<b>Features:</b>
<ul><li>Works with many different ultrasonic sensor models: SR04, SRF05, SRF06, DYP-ME007 & Parallax PING)))™.<br>
</li><li>Option to interface with all but the SRF06 sensor <a href='http://code.google.com/p/arduino-new-ping/wiki/NewPing_Single_Pin_Sketch'>using only one Arduino pin</a>.<br>
</li><li><u>Doesn't lag for a full second</u> if no ping echo is received like all other ultrasonic libraries.<br>
</li><li>Ping sensors consistently and reliably at up to <u>30 times per second</u>.<br>
</li><li><a href='http://code.google.com/p/arduino-new-ping/wiki/Ping_Event_Timer_Sketch'>Timer interrupt method</a> for event-driven sketches.<br>
</li><li>Built-in <a href='http://code.google.com/p/arduino-new-ping/wiki/Using_NewPing_Syntax'>digital filter method ping_median()</a> for easy error correction.<br>
</li><li>Uses port registers when accessing pins for <u>faster execution and smaller code size</u>.<br>
</li><li>Allows <a href='http://code.google.com/p/arduino-new-ping/wiki/Using_NewPing_Syntax'>setting of a maximum distance</a> where pings beyond that distance are read as no ping "clear".<br>
</li><li>Ease of using multiple sensors (<a href='http://code.google.com/p/arduino-new-ping/wiki/15_Sensors_Example'>example sketch that pings 15 sensors</a>).<br>
</li><li><u>More accurate distance calculation</u> (cm, inches & microseconds).<br>
</li><li><u>Doesn't use pulseIn</u>, which is slow and gives incorrect results with some ultrasonic sensor models.<br>
</li><li>Actively developed with features being added and bugs/issues addressed.<br>
<br>
<b>Download: <a href='http://code.google.com/p/arduino-new-ping/downloads/list'>Download NewPing v1.5</a></b>
<br></li></ul>

<b>Download: <a href='http://code.google.com/p/arduino-new-ping/wiki/BetaDownload'>Download NewPing v1.6 BETA</a></b>
<br><br>

<b>Example: <a href='http://code.google.com/p/arduino-new-ping/wiki/Simple_NewPing_Example'>Simple NewPing Example Sketch</a></b>
<br><br>

<b>Syntax: <a href='https://code.google.com/p/arduino-new-ping/wiki/Using_NewPing_Syntax'>NewPing Syntax</a></b>
<br><br>

<b>Show Your Appreciation:</b> Help future development by making a small donation (yes, the FreeRingers payee is correct).<br>
<a href='https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=5KUFX27CEZX5L'><img src='https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif' /></a>
<br>
<b>Supporters:</b>
<br>Weyman S. $5.00 5/8<br>
<br>Bob R. $5.00<br>
<br>Zdenek K. $10.00<br>
<br>Duane G. $10.00<br>
<br>Ronald B. (Granpa) $20.00<br>
<br><a href='http://www.emworkbench.com/'>EM Workbench</a> $25.00<br>
<br>Ralph H. $25.00<br>
<br>Ron T. $5.00<br>
<br>Greg S. $5.00<br>
<br>William M. $10.00<br>
<br>Douglas M. $5.00<br>
<br>Nikita V. $3.00<br>
<br>Matthew B. $10.00<br>
<br>Olexiy L. $10.00<br>
<br>Matt K. $3.00<br>
<br>Charles D. $10.00<br>
<br>Frédérik B. $5.00<br>
<br><a href='http://yourduino.com/'>YourDuino.com</a> $10.00<br>
<br>Silva M. $10.00<br>
<br>David B. $10.00<br>
<br>Lukas M. $2.00<br>
<br>Jonas H. $2.50<br>
<br>Graeme M. $5.00<br>
<br>Alessandro Z. $20.00<br>
<br>Maximilian S. $10.00<br>
<br>Wally H. - $5.00<br>
<br>Debottam B. - $2.00<br>
<br>Tim H. - $20.00<br>
<br>Paul M. - $5.00<br>
<br>James W. - $10.00<br>
<br>Isaac R. - $2.00<br>
<br>Erica S. - $10.00<br>
<br>
<img src='http://www.leethost.com/link_pics/2wire_bb.png' />

<b>Scheduled for Release in v1.6: (<a href='http://code.google.com/p/arduino-new-ping/wiki/BetaDownload'>Download NewPing v1.6 BETA</a>)</b>
<ul><li>ping_interrupt() method which uses external pin interrupt to measure distance with no polling overhead.<br>
</li><li>More accurate ping_median() method.<br>
</li><li>Added support for URM37 sensors.<br>
</li><li>Added support for the Arduino Due and other ARM-based microcontrollers (like $19 96MHz Teensy 3.x).<br>
</li><li>Automatic support for Atmel ATtiny family of microcontrollers.<br>
</li><li>Added timer support for the ATmega8 microcontroller.<br>
</li><li>Reduction of compiled code size.<br>
</li><li>Speed optimizations.<br>
</li><li>Switch for compatibility with Tone library (or just use my <b><a href='https://code.google.com/p/arduino-new-tone/'>NewTone</a></b> or <b><a href='http://code.google.com/p/arduino-tone-ac'>toneAC</a></b> libraries).</li></ul>

<h2>Cool User Projects Using NewPing</h2>
<table><thead><th> <img src='http://www.leethost.com/link_pics/newping1.jpg' /> </th><th> <img src='http://www.leethost.com/link_pics/newping2.jpg' /> </th></thead><tbody>
<tr><td> <a href='http://www.youtube.com/watch?feature=player_embedded&v=j7E5ZT2hEI0' target='_blank'><img src='http://img.youtube.com/vi/j7E5ZT2hEI0/0.jpg' width='425' height=344 /></a> </td></tr></tbody></table>

<b>New in v1.5 - Released 8/15/2012:</b><br>
Added ping_median() method which does a user specified number of pings (default=5) and returns the median ping in microseconds (out of range pings ignored). This is a very effective digital filter. Optimized for smaller compiled size (even smaller than sketches that don't use a library).<br>
<br>
<b>New in v1.4 - Released 7/14/2012:</b><br>
You can now interface with all but the SRF06 sensor using only one Arduino pin. Added support for the Parallax PING)))™ sensor. You can also interface with the SRF06 using one pin if you install a 0.1uf capacitor on the trigger and echo pins of the sensor then tie the trigger pin to the Arduino pin (doesn't work with Teensy). To use the same Arduino pin for trigger and echo, specify the same pin for both values. Various bug fixes.<br>
<br>
<b>New in v1.3 - Released 6/8/2012:</b><br>
Big feature addition, event-driven ping! Uses Timer2 interrupt, so be mindful of PWM or timing conflicts messing with Timer2 may cause (namely PWM on pins 3 & 11 on Arduino, PWM on pins 9 and 10 on Mega, and Tone library). Simple to use timer interrupt functions you can use in your sketches totaly unrelated to ultrasonic sensors (don't use if you're also using NewPing's ping_timer because both use Timer2 interrupts). Loop counting ping method deleted in favor of timing ping method after inconsistant results kept surfacing with the loop timing ping method. Conversion to cm and inches now rounds to the nearest cm or inch. Code optimized to save program space and fixed a couple minor bugs here and there. Many new comments added as well as line spacing to group code sections for better source readability.<br>
<br>
NOTE: For Teensy/Leonardo (ATmega32U4) the library uses Timer4 instead of Timer2.  Also, only 16Mhz microcontrollers are supported with the timer methods, which means the ATmega8 and ATmega128 will not work with the timer methods.  However, the standard ping method should work just fine on 8Mhz microcontrollers.<br>
<br>
<b>New in v1.2 - Released 5/24/2012:</b><br>
Lots of code clean-up thanks to Adruino Forum members. Rebuilt the ping timing code from scratch, ditched the pulseIn code as it doesn't give correct results (at least with ping sensors). The NewPing library is now VERY accurate and the code was simplified as a bonus. Smaller and faster code as well. Fixed some issues with very close ping results when converting to inches. All functions now return 0 only when there's no ping echo (out of range) and a positive value for a successful ping. This can effectively be used to detect if something is out of range or in-range and at what distance. Now compatible with Arduino 0023.<br>
<br>
<b>New in v1.1 - Released 5/16/2012:</b><br>
Changed all I/O functions to use low-level port registers for ultra-fast and lean code (saves from 174 to 394 bytes). Tested on both the Arduino Uno and Teensy 2.0 but should work on all Arduino-based platforms because it calls standard functions to retrieve port registers and bit masks.  Also made a couple minor fixes to defines.<br>
<br>
<b>v1.0 - Released 5/15/2012:</b><br>
Initial release.