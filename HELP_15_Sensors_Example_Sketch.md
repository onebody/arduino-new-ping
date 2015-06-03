# HELP - 15 Sensors Example Sketch #

There's been some confusion about how to use the 15 Sensors Example Sketch.  I've changed some of the comments in the online code to help.  But, I think a post explaining this further would be beneficial.

The 15 Sensors Example Sketch uses the ping\_timer() method which is designed for event-driven sketches that don't use delays.  If you're only used to Arduino sketches that are linear and have delays in the code, this concept will be quite foreign to you.  However, it's a good idea to try and embrace an event-driven paradigm.  Simple example "hello world" sketches work fine using delays.  But, once you try to do a complex project, using delays will often result in a project that just doesn't do what you want.  Consider controlling a motorized robot with remote control that balances and using ping sensors to avoid collisions.  Any delay at all, probably even 1 ms, would cause the balancing to fail and therefore your project would never work.  In other words, it's a good idea to start not using delays at all, or you're going to have a really hard time getting your project off the ground (literally with the balancing robot example).

So, it's good to first note that the 15 sensor example doesn't use any delays and is event driven.  You can think of it as multitasking.  The for() loop in void() polls each sensor array waiting for when it's that sensor's time to ping.  If it's time to ping, it triggers a ping\_timer() to run in the background.  After the for() loop in void() where the comment is, you could add other code here that doesn't have anything to do with ping sensors.  For example: monitoring other sensors, controlling status lights, or whatever.  But, it's VERY important that these other things are also designed in an event-driven way with no delays.  If you add delays, it will miss ping times and skip them, resulting in what appears to be an error.

echoCheck() is where the background ping is polled every 24uS to see if a ping was received. If a ping is received, it sets the ping distance in CM in the cm[.md](.md) array.  You shouldn't add anything to echoCheck() to use this sketch in its designed way.  This function always needs to be very lean as it's called every 24uS during a ping.

oneSensorCycle() is called once all of your sensors have been polled.  Lets say you have 8 sensors.  Every time all 8 sensors are pinged, this function is called and you can do something with the results.  For example, determine the surroundings of your robot and maybe make a motor direction change.  It doesn't have to output the results over a serial connection, this is just here for testing.  In a real-world sketch, you would remove or comment out everything in the oneSensorCycle() function and replace it with your code that does something with the sensor data in the cm[.md](.md) array.

Also note, the 15 Sensors Example Sketch is designed to ping all the sensors and then do something with the results once all the sensors have been polled.  Some want to ping each sensor and then do something right away maybe between any two pings.  To do that, we no longer need the oneSensorCycle() function nor the if() statement in loop() that calls oneSensorCycle().  The following sketch calls the pingResult() function every time there's a ping within range.  Because this sketch still keeps the cm[.md](.md) array, you can look at neighboring ping results in the cm[.md](.md) array to do whatever calculations you need to do.

```
#include <NewPing.h>

#define SONAR_NUM      3 // Number of sensors.
#define MAX_DISTANCE 200 // Maximum distance (in cm) to ping.
#define PING_INTERVAL 33 // Milliseconds between sensor pings (29ms is about the min to avoid cross-sensor echo).

unsigned long pingTimer[SONAR_NUM]; // Holds the times when the next ping should happen for each sensor.
unsigned int cm[SONAR_NUM];         // Where the ping distances are stored.
uint8_t currentSensor = 0;          // Keeps track of which sensor is active.

NewPing sonar[SONAR_NUM] = {   // Sensor object array.
  NewPing(4, 5, MAX_DISTANCE), // Each sensor's trigger pin, echo pin, and max distance to ping.
  NewPing(6, 7, MAX_DISTANCE),
  NewPing(8, 9, MAX_DISTANCE)
};

void setup() {
  Serial.begin(115200);
  pingTimer[0] = millis() + 75;           // First ping starts at 75ms, gives time for the Arduino to chill before starting.
  for (uint8_t i = 1; i < SONAR_NUM; i++) // Set the starting time for each sensor.
    pingTimer[i] = pingTimer[i - 1] + PING_INTERVAL;
}

void loop() {
  for (uint8_t i = 0; i < SONAR_NUM; i++) { // Loop through all the sensors.
    if (millis() >= pingTimer[i]) {         // Is it this sensor's time to ping?
      pingTimer[i] += PING_INTERVAL * SONAR_NUM;  // Set next time this sensor will be pinged.
      sonar[currentSensor].timer_stop();          // Make sure previous timer is canceled before starting a new ping (insurance).
      currentSensor = i;                          // Sensor being accessed.
      cm[currentSensor] = 0;                      // Make distance zero in case there's no ping echo for this sensor.
      sonar[currentSensor].ping_timer(echoCheck); // Do the ping (processing continues, interrupt will call echoCheck to look for echo).
    }
  }
  // Other code that *DOESN'T* analyze ping results can go here.
}

void echoCheck() { // If ping received, set the sensor distance to array.
  if (sonar[currentSensor].check_timer()) {
    cm[currentSensor] = sonar[currentSensor].ping_result / US_ROUNDTRIP_CM;
    pingResult(currentSensor);
  }
}

void pingResult(uint8_t sensor) { // Sensor got a ping, do something with the result.
  // The following code would be replaced with your code that does something with the ping result.
  Serial.print(sensor);
  Serial.print(" ");
  Serial.print(cm[sensor]);
  Serial.println("cm");
}
```

If, however, you don't really care about comparing neighboring ping results and just want to ping multiple sensors and anytime there's something within range you want to trigger something, you can totally get rid of the cm[.md](.md) array.  The following code is probably the easiest to understand, as it simply pings each sensor and when there's a ping within range, the pingResult() function is called.  You get the sensor number and the cm distance which you can do something with.  It will only call pingResult() when one of the sensors "hears" something within range.

```
#include <NewPing.h>

#define SONAR_NUM      3
#define MAX_DISTANCE 200
#define PING_INTERVAL 33

unsigned long pingTimer[SONAR_NUM];
uint8_t currentSensor = 0;

NewPing sonar[SONAR_NUM] = {
  NewPing(4, 5, MAX_DISTANCE),
  NewPing(6, 7, MAX_DISTANCE),
  NewPing(8, 9, MAX_DISTANCE)
};

void setup() {
  Serial.begin(115200);
  pingTimer[0] = millis() + 75;
  for (uint8_t i = 1; i < SONAR_NUM; i++)
    pingTimer[i] = pingTimer[i - 1] + PING_INTERVAL;
}

void loop() {
  for (uint8_t i = 0; i < SONAR_NUM; i++) {
    if (millis() >= pingTimer[i]) {
      pingTimer[i] += PING_INTERVAL * SONAR_NUM;
      sonar[currentSensor].timer_stop();
      currentSensor = i;
      sonar[currentSensor].ping_timer(echoCheck);
    }
  }
  // Other code that *DOESN'T* analyze ping results can go here.
}

void echoCheck() {
  if (sonar[currentSensor].check_timer())
    pingResult(currentSensor, sonar[currentSensor].ping_result / US_ROUNDTRIP_CM);
}

void pingResult(uint8_t sensor, int cm) {
  // The following code would be replaced with your code that does something with the ping result.
  Serial.print(sensor);
  Serial.print(" ");
  Serial.print(cm);
  Serial.println("cm");
}
```

Remember, to analyze the ping results, you do that in the pingResults() function in the above sketches or in the oneSensorCycle() function in the 15 Sensors Example Sketch.  Also, none of these will properly work if you do any delay statements at any point in your sketch.

If you ever want to stop the pings in your sketch, for example to do something that requires delays or takes longer than 33ms to process, do the following:

```
for (uint8_t i = 0; i < SONAR_NUM; i++) pingTimer[i] = -1;
```

To start the pings again, do the following:

```
pingTimer[0] = millis();
for (uint8_t i = 1; i < SONAR_NUM; i++) pingTimer[i] = pingTimer[i - 1] + PING_INTERVAL;
```

Hope this helps!