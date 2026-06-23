# CS350_Emerging_SYS
# Smart Thermostat Prototype - CS 350 Final Project

## Project Overview

This repository contains embedded systems code for a smart thermostat prototype developed for SysTec Analytics. The project addresses the challenge of creating a low-level thermostat control system with cloud connectivity potential. The prototype demonstrates a three-state heating/cooling system that reads environmental data via I2C sensors, provides user feedback through PWM-controlled LEDs and an LCD display, accepts user input through GPIO buttons, and transmits status data via UART serial communication.

The thermostat solves the problem of how to effectively manage room temperature control while providing real-time feedback to users and external systems. Beyond basic on/off control, the system intelligently manages heating and cooling states, allows dynamic temperature setpoint adjustment, and displays critical information on an integrated display—all requirements for modern smart home integration.

## What I Did Particularly Well

I successfully implemented a robust state machine architecture that cleanly separated concerns between state management, hardware control, and user interface. The three-state design (off, heating, cooling) proved elegant and extensible, making it straightforward to add additional states or behaviors. The state machine's event-driven approach ensured that button presses were handled responsively without blocking critical operations like display updates or temperature sensor reads.

The integration of multiple hardware interfaces demonstrated solid understanding of embedded systems design. I successfully coordinated I2C communication with the temperature sensor, PWM control for LED brightness effects, GPIO interrupt handling for buttons, UART serial output, and LCD display management—all running concurrently through threading. This multi-interface coordination, while complex, worked reliably throughout testing.

I also demonstrated strong problem-solving when encountering hardware issues. When the temperature sensor initially failed to respond on the I2C bus, I systematically diagnosed the problem (loose QWIIC cable connections), verified the issue through direct testing (`i2cdetect`), and confirmed the fix—skills that are essential in real embedded systems work where hardware and software problems often intertwine.

## Where I Could Improve

The code would benefit from additional error handling and recovery mechanisms. While the state machine is robust, the sensor reading operations lack fallback behavior if the I2C bus becomes temporarily unavailable. In production, the system should gracefully degrade and attempt to re-establish connections rather than crashing.

The display update logic could be more efficient. Currently, the entire display refreshes every second regardless of whether the content changed. Implementing a change-detection system would reduce unnecessary I2C writes to the LCD, improving responsiveness and reducing power consumption—critical considerations for battery-powered thermostat deployment.

Additionally, the code would benefit from more comprehensive unit testing. While I tested functionality manually, structured unit tests for critical functions like temperature conversion and state transitions would increase confidence in the system's reliability and make future modifications safer.

## Tools and Resources Added to My Support Network

This project introduced me to several tools that I'll continue using:

**Hardware Debugging Tools:** `i2cdetect` proved invaluable for diagnosing I2C bus issues. I now have a systematic approach to hardware troubleshooting that I'll apply to future embedded projects.

**State Machine Libraries:** The Python `statemachine` library elegantly solved state management problems. I appreciate how it forces explicit thinking about states and transitions, and I'll seek similar tools in other languages.

**Serial Communication Debugging:** Understanding UART communication at a protocol level (baud rates, encoding, serial port configuration) has given me confidence working with serial devices beyond just the Raspberry Pi.

**Version Control and Documentation:** Using GitHub to organize and document embedded systems projects has improved my portfolio presentation and will help me maintain code over time.

## Skills Transferable to Other Projects

The state machine design pattern is universally applicable—traffic lights, game logic, workflow systems, and user interface flows all benefit from explicit state management. This project cemented my understanding of how to think in states and transitions.

Multi-threaded programming in Python is directly transferable. I learned how to safely coordinate multiple concurrent operations without blocking critical paths. This skill applies to any system managing real-time input and output.

Hardware integration skills are perhaps most transferable. The systematic approach to connecting sensors, actuators, and displays transfers directly to other embedded projects, whether using Raspberry Pi, Arduino, or commercial microcontrollers.

Finally, the problem-solving methodology itself—defining requirements, prototyping, testing, diagnosing failures, and iterating—is applicable across all software and hardware projects. This course reinforced that systematic thinking is more valuable than knowing specific tools.

## Maintainability, Readability, and Adaptability

I prioritized code readability through consistent naming conventions, comprehensive comments explaining the purpose of each function and state, and logical organization separating concerns into distinct methods and classes.

The state machine design inherently improves maintainability. Adding new states (like a vacation mode or eco mode) requires only adding a new State object and defining its behavior—no refactoring of existing logic. The event-driven approach means changes to button behavior are isolated to specific methods.

I made the code adaptable by using GPIO pin assignments as clearly defined constants at the top of the file, making it trivial to change hardware pin mappings without searching through code. Temperature thresholds and display update intervals are similarly exposed as configurable values.

The ManagedDisplay class encapsulates all LCD-related operations, allowing the display implementation to be completely replaced (e.g., swapping for an OLED or web-based interface) without touching the thermostat logic.

Threading use, while adding complexity, actually improves adaptability. The separation of display management and temperature sensing into independent threads means new features can be added as additional threads without disrupting existing functionality.

---

## Files Included

- **Thermostat.py** - Final smart thermostat implementation with state machine architecture
- **README.md** - This documentation file
- **Hardware_Architecture_Report.docx** - Analysis of hardware options for production deployment

