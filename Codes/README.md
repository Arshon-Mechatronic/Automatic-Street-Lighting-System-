#include <pic.h>
// Define sensor and actuator pins
#define SENSOR_PIN RB0
#define RELAY_PIN RB1
#define PWM_PIN CCPR1L
void main() {
 TRISB0 = 1; // Set sensor pin as input
 TRISB1 = 0; // Set relay pin as output
 TRISC2 = 0; // Set PWM pin as output
 // Configure PWM
 CCP1CON = 0b00001100; // PWM mode
 T2CON = 0b00000101; // Enable TMR2 with prescaler 4
 while(1) {
 if(SENSOR_PIN == 1) {
 // Vehicle detected, switch to 100% intensity
 PWM_PIN = 255; // Set PWM duty cycle to 100%
 RELAY_PIN = 1; // Turn on street lights
 } else {
 // No vehicle, switch to 10% intensity
 PWM_PIN = 25; // Set PWM duty cycle to 10%
 RELAY_PIN = 0; // Turn off street lights
 }
 }
}
