# Using NewPing (Syntax) #

  * **`NewPing sonar(trigger_pin, echo_pin [, max_cm_distance]);`** - Initialize an ultrasonic device, trigger pin, echo pin, and [optional](optional.md) maximum distance you wish to sensor to measure (default = 500cm).


  * **`sonar.ping();`** - Send a ping and get the echo time (in microseconds) as a result.
  * **`sonar.ping_in();`** - Send a ping and get the distance in whole inches.
  * **`sonar.ping_cm();`** - Send a ping and get the distance in whole centimeters.
  * **`sonar.ping_median(iterations);`** - Do multiple pings (default=5), discard out of range pings and return median in microseconds.
  * **`sonar.convert_in(echoTime);`** - Convert echoTime from microseconds to inches.
  * **`sonar.convert_cm(echoTime);`** - Convert echoTime from microseconds to centimeters.

  * **`sonar.ping_timer(function);`** - Send a ping and call function to test if ping is complete.
  * **`sonar.check_timer();`** - Check if ping has returned within the set distance limit.

  * **`NewPing::timer_us(frequency, function);`** - Call function every frequency microseconds.
  * **`NewPing::timer_ms(frequency, function);`** - Call function every frequency milliseconds.
  * **`NewPing::timer_stop();`** - Stop the timer.