# XRP Robot Programming

## Review command-based program structure

There are two fundamental architectures that you will see in First Robotics code - functional "TimedRobot" and Command based programming.

Functional programming is when you micro-manage every aspect of the program's execution, such as when sensors are checked, what happens when a timer is waiting for an event, and when motor drivers are updated.

In command-based programming, many of these processes are taken care of in the background without the programmer having to manage them.  It does take a little more effort to set up, but it vastly improves your program's ability to do multiple operations at once.

Consider the following situation:
You have a robot with a simple differential drive base and a shooter to throw a ball at a target.  Your drive team wants to have the robot drive to the next pickup location while the shooter is tracking and taking a shot at the scoring goal.

With functional programming, you have to manage constantly switching between both tasks.  You monitor the drive base position, adjust the robot's drive trajectory and speed.  Then you check the tracking location of the goal, the position of the robot, and the speed of the flywheels on the shooter.  This process is repeated with different decision points along the path.

With command-based (object-oriented) programming, the tasks are treated separately in the code.  One part drives the robot to the desired position, and the other part makes a shot at the goal.  It seems like both tasks are executing at the same time, but actually the computer is constantly switching between tasks.  This drastically reduces the complexity that the programmer has to manage and passes it off to the computer, which is very good at it.

> ### Example Functional Coding:
> [Timed Robot](https://github.com/wpilibsuite/allwpilib/blob/main/wpilibjExamples/src/main/java/edu/wpi/first/wpilibj/examples/arcadedrive/Robot.java)
> ### Example Command-based Coding:
> [Object Oriented Code](https://github.com/wpilibsuite/allwpilib/tree/main/wpilibjExamples/src/main/java/edu/wpi/first/wpilibj/examples/drivedistanceoffboard)

## Auto routine structure
Pull up your XRP robot code.  You are going to create your own command.  Find the "commands" directory and right click on it.  At the bottom of the list you will see "Create a new class/command".  Then select "Command" and name it "TurnToAngle".

![New Command](Lesson02_visuals\NewCommand.png)

![Select Command](Lesson02_visuals\SelectCommand.png)

```java
public class TurnToAngle extends Command {
  /** Creates a new TurnToAngle. */
  public TurnToAngle() {
    // Use addRequirements() here to declare subsystem dependencies.
  }

  // Called when the command is initially scheduled.
  @Override
  public void initialize() {}

  // Called every time the scheduler runs while the command is scheduled.
  @Override
  public void execute() {}

  // Called once the command ends or is interrupted.
  @Override
  public void end(boolean interrupted) {}

  // Returns true when the command should end.
  @Override
  public boolean isFinished() {
    return false;
  }
}
```

## Investigate "DriveTime"
How does this command work?
* Explain what it does and how it ends.
* How is it different from DriveDistance?
* TurnTime is similar to DriveTime, but explain how TurnDegrees determines how it is finished.

## Sequential Command Groups
* Investigate "AutonomousTime"
* Investigate "AutonomousDistance"
* Explain how they work

## Test different auto commands
Turn on your robot.  Let's try out the two different routines.
* Auto Routine Distance
* Auto Routine Time

Explore, modify and experiment for a bit.

> ### Challenge:
> Modify one of the Autonomous routines to move the robot in a square, and return to where it started.

## Turning the robot to a sensor
Using the other autonomous commands as a guide, you are going to add code to your TurnToAngle command that will turn the robot to an angle on the gyroscope.

Hints:
* You will be passing in a reference to the drivetrain like the other commands.  Once you have that, you can access the gyroscope angle by calling the function: `m_drive.GetGyroAngleZ()`
* In initialize, you will need to reset the gyro angle to zero: `m_drive.resetGyro()`
* Which direction is positive degrees?
* How does the command stop?

Test your program by substituting the `TurnToAngle` command in one of the Sequential Command Groups.

> ### Challenge:
> Figure out how to trigger your autonomous routine in Teleop mode by binding the routine to a joystick button. Hint: Use RobotContainer.

#### Resources
* [https://docs.wpilib.org](https://docs.wpilib.org)
* [https://www.learncs.online/lessons](https://www.learncs.online/lessons)
* [Rev Timed Robot](https://github.com/REVrobotics/REVLib-Examples/blob/main/Java/SPARK/Open%20Loop%20Arcade%20Drive/src/main/java/frc/robot/Robot.java)
* [CTR Timed Robot](https://github.com/CrossTheRoadElec/Phoenix6-Examples/blob/main/java/VelocityClosedLoop/src/main/java/frc/robot/Robot.java)
