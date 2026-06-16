This is a pretty clever way of understanding algo and is helpful to quickly brainstorm and turn this diagram into working code. 

There are some key parts for this diagram: 
![[Screenshot 2025-09-18 at 0.18.20.png]]

Here is also an example of how structograms compare to code and flowcharts;![[Screenshot 2025-09-18 at 0.19.05.png]]

There are 2 ways to write a loop here, 
1. Top-test loop or test-first loop ![[Screenshot 2025-09-18 at 0.21.59.png|500]] ^toptest
   * Here the condition is checked first and then the loop is executed
   * Output for this would be,
	   * nil _since we have x=7 and the first conditional is x<6 which it doesnt satisfy, the loop simply wont happen, the program directly ends._
1. Bottom-test loop or test-last loop![[Screenshot 2025-09-18 at 0.24.08.png|500]]^bottomtest
   * Here the condition is checked at last, after the 1st loop is executed.
   * The output for this would be
	   * 7 + 4 = 11
	   * nil
		   * _here although all the numbers are the same, the process takes x, adds 4, displays on the screen and only then checks if x < 6, so, the first output is displayed before the check even happens._

   