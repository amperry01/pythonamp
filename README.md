# pythonamp

#!/usr/bin/env python3
"""
    This is a good foundation to build your robot code on
"""

import wpilib

class MyRobot(wpilib.IterativeRobot):

    def robotInit(self):
        """
        This function is called upon program startup and
        should be used for any initialization code.
        """
        self.robot_drive = wpilib.RobotDrive(0, 1, 2, 3)
        self.stick = wpilib.Joystick(1)

    def autonomousInit(self):
        """This function is run once each time the robot enters autonomous mode."""
        self.auto_loop_counter = 0

    def autonomousPeriodic(self):
        """This function is called periodically during autonomous."""

        # Check if we've completed 100 loops (approximately 2 seconds)
        if self.auto_loop_counter < 100:
            self.robot_drive.tankDrive(-0.5, -0.5) # Drive forwards at half speed
            self.auto_loop_counter += 1
        elif self.auto_loop_counter >= 100 & self.auto_loop_counter < 200:
            self.robot_drive.tankDrive(-0.5, 0.5)  #hopefully turns robot
            self.auto_loop_counter += 1   
        else:
            self.robot_drive.drive(0, 0)    #Stop robot

    def teleopPeriodic(self):
        """This function is called periodically during operator control."""
        self.robot_drive.mecanumDrive_Cartesian(self.stick.getX(), self.stick.getY(), self.stick.getZ(), 0)

    def testPeriodic(self):
        """This function is called periodically during test mode."""
        wpilib.LiveWindow.run()

if __name__ == "__main__":
    wpilib.run(MyRobot)
