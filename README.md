# Wiring

# APPS

5V input/output. Use a voltage divider/other approach to condition the analogue output to a range that can be read by ESP32

# TPS


# Nema 23 Stepper motor

https://www.motechmotor.com/productDetail-0105-81.html

step angle $1.8\degree$

# TMC5160 driver board

datasheet: [TMC5160 Datasheet (long))](https://www.analog.com/media/en/technical-documentation/data-sheets/TMC5160A_datasheet_rev1.18.pdf)

Description: [TMC5160 BOB Description](https://www.analog.com/media/en/technical-documentation/data-sheets/tmc5160-bob_datasheet_rev1.10.pdf)

Install this library developed by tommag. both `TMC5160.h` and `Bitfield.h` are included

https://github.com/tommag/TMC5160_Arduino

# Motor torque

Adjust motor torque by writing to these registers (in setup, after SPI communication and motor has been initialised):

```
  motor.writeRegister(TMC5160_Reg::GLOBAL_SCALER, 200); //32-255
  motor.writeRegister(TMC5160_Reg::IHOLD_IRUN, 0x00011F14);
```

The complete list of register can be found in /TMC5160_registers.h

The `IHOLD_IRUN` register format:

* Bits 0-4: ihold (in this case hex(14) = dec(20))(0-31) (set to <= 70% of irun)
* Bits 8-12: irun (0-31)
* Bits 16-19: iholddelay

! For some reasons changing motorParams didn't work for me. had to write to register for the change to stick

## Resources

- [PID Controller in C](https://deepbluembedded.com/esp32-timers-timer-interrupt-tutorial-arduino-ide/)
- [ESP32 Arduino IDE Timer Interrupts Reference](https://deepbluembedded.com/esp32-timers-timer-interrupt-tutorial-arduino-ide/)
