# FRC_2026_SoftwareLessons

This is just an outline of the season lessons for now.  It will eventually be removed.

Requirements for Test code:
* open loop speed control for motors
* Turn to degree mode for motors
* Encoder feedback
* Turn to position mode
* Safe operating speeds
* Operates all motors in our inventory (individually)
* diagnostic data: voltage, current, motor capacity, battery internal resistance estimate, temperature

Electrical/programming kit for competition:
* checklist for robot cart
    * Ethernet cable spool & patch cable
    * Long USB-C cable for motor driver programming (orange)
    * USB-C to Ethernet dongle for laptop
* checklist for pit
* checklist for software team cart
    * video presentation cable (long HDMI cable with FRC logo)

Season updates / inventory
* Verify operation of all joysticks

Java coding
* Basic Structure / syntax
* Data types
* Simple code/print
* VS Code / Git
* conditional/loops
* comments/ readable/code review

WPILib coding
* Basic structure
* Motor structure
* controller programming
* motor programming
    * vendor software for motor drivers
* mechanisms
* competition know-how: direct ethernet connection to robot, radio programming, battery hygene

Test of a season schedule chart:
```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title       Robotics Season Schedule
    excludes    weekends, sunday, monday, wednesday, friday
    %% (`excludes` accepts specific dates in YYYY-MM-DD format, days of the week ("sunday") or "weekends", but not the word "weekdays".)
    %% https://mermaid.js.org/intro/

    todayMarker stroke-width:5px,stroke:#0f0,opacity:0.5

    section Pre-Season
    Early meetings  :done,  ps01, 2025-10-07, 2025-10-09
    Prep for Open House :active, ps02, 2025-10-14, 1d
    Open House  :milestone, ps03, 2025-10-16, 1min
    Remaining pre-Season    : ps04, 2025-10-21, 2025-10-23

    section Critical tasks
    Create git codebase for 2026    :active, cr01, 2025-10-16, 1d
    Swerve module code  :active, cr02, after cr01, 2d
    Plan mechanisms :until isadded
    Code mechanisms :milestone, isadded, 2025-10-25, 0d

    section Events
    Kickoff :milestone, ev_kickoff, 2026-01-03, 1min
    %%Seven Rivers (La Crosse)    :milestone, ev_7rivers, 2026-04-02, 2026-04-04
    %%LRR :milesone, ev_lrr, after ev_7rivers, 1min

    section Outreach Events
    Science Fest    :milestone, 2025-10-17, 2h
```

Test Class Diagram
```mermaid
---
title Generic Robot Code (Kitbot 2025)
---
classDiagram
    RobotContainer <|-- DriveSubsystem
    RobotContainer <|-- RollerSubsystem
    RobotContainer <|-- AutoCommand
    RobotContainer <|-- AutoScoreCoral
    DriveSubsystem <-- AutoCommand
    DriveSubsystem <-- AutoScoreCoral
    RollerSubsystem <-- AutoScoreCoral
    RobotContainer : +CommandXboxController driverController
    RobotContainer: -configureBindings()

    namespace Subsystems{
    class DriveSubsystem{
        -SparkMax leftLeader
        -SparkMax leftFollower
        -SparkMax rightLeader
        -SparkMax rightFollower
        -RelativeEncoder m_EncoderLeft
        -RelativeEncoder m_EncoderRight
        -DifferentialDrive drive

        -getEncoderMeters(RelativeEncoder enc)
        +driveArcade(double xSpeed, double zRotation)
        +getHeading()
    }
    class RollerSubsystem{
        -TalonSRX rollerMotor
        +runRoller(double forward, double reverse)
    }
    }
    namespace Commands {
        class AutoCommand{
        }
        class AutoScoreCoral{
        }
    }
```