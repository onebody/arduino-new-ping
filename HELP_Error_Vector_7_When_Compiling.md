# HELP - Multiple Definition of `vector\_7' Error When Compiling #

A common problem with using NewPing is getting a `vector\_7' error during compile.  What this error means is that you're using two libraries that are both trying to use timer 2.  The timer 2 stuff is only in NewPing for the timer interrupt method ping\_timer().  If you're just using the standard ping(), ping\_in(), ping\_cm(), or ping\_median() methods, NewPing is not using timer 2.  However, the compiler is not smart enough to know that you're not using those interrupts. So you'll get this error if any other library is also using timer 2.

There's an easy solution as long as you're not using ping\_timer().  Change the NewPing.cpp program and comment out the section that calls timer 2.  Find this section at around lines 210 - 216 in version 1.5:

```
#if defined (__AVR_ATmega32U4__) // Use Timer4 for ATmega32U4 (Teensy/Leonardo).
ISR(TIMER4_OVF_vect) {
#else
ISR(TIMER2_COMPA_vect) {
#endif
	if(intFunc) intFunc(); // If wrapped function is set, call it.
}
```

Comment it all out like this:

```
/*
#if defined (__AVR_ATmega32U4__) // Use Timer4 for ATmega32U4 (Teensy/Leonardo).
ISR(TIMER4_OVF_vect) {
#else
ISR(TIMER2_COMPA_vect) {
#endif
	if(intFunc) intFunc(); // If wrapped function is set, call it.
}
*/
```

That's it!  Also, if the conflict is with the tone library, you can use a different tone library that doesn't use timer 2.  I've created a couple tone replacement libraries that not only use timer 1 instead of timer 2 to avoid a conflict, they also have many other advantages:

**[NewTone](https://code.google.com/p/arduino-new-tone/)** - About 1,200 bytes smaller code size than the standard tone library. Faster execution time. Exclusive use of port registers for fastest and smallest code. Higher quality sound output than tone library. Plug-in replacement for Tone. Uses timer 1 which may free up conflicts with the tone library.

**[toneAC](https://code.google.com/p/arduino-tone-ac/)** - Nearly twice the volume (because it uses two out of phase pins in push/pull fashion). Higher quality (less clicking). Capability of producing higher frequencies (even if running at a lower clock speed). Nearly 1.5k smaller compiled code. Bug fixes (standard tone library can generate some odd and unpredictable results). Can set not only the frequency but also the sound volume. Less stress on the speaker so it will last longer and sound better.

**[TimerFreeTone](https://code.google.com/p/arduino-timer-free-tone/)** - Doesn't use timers which frees up conflicts with other libraries.  Compatible with all ATmega, ATtiny and ARM-based microcontrollers.  Over 1,500 bytes smaller binary sketch size than the standard tone library.  Exclusive use of port registers for AVR-based microcontrollers for fastest and smallest code.  Close to a plug-in replacement for the standard Tone library.

In addition, version 1.6 of the NewPing library (currently being released as beta) includes the TIMER\_ENABLED switch that allows you to easily turn off the timer 2 stuff if you're not using the ping\_timer() method.

If, however you are using the ping\_timer() method you still may have options.

First, do you really need to use the ping\_timer() method?  Many people incorrectly assume that if they're using multiple sensors they must use the ping\_timer() method shown in my 15 sensor example.  That's simply not the case.  It's best to do it that way for "multitasking" reasons.  But, there's no reason why you can't just ping() multiple sensors like in the NewPingExample sketch.

Secondly, maybe you can use a different library that's causing the timer 2 conflict.  I've shown two other tone libraries above that use timer 1 instead of timer 2.  But, if the timer 2 conflict is with a different library, there's still a chance that you have another option.  For example, maybe the timer 2 conflict is with an LED dimmer library.  Try to find another LED dimmer library that uses timer 1 instead.  While this may not be an option for every library, there are many libraries out there so it's worth looking into.