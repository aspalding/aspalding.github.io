---
layout: post
title: "Open Closed Principal"
date: 2014-06-19
---

OCP (Open-Closed Principal) relates to object orientated and agile design. It is defined in [PPP][ppp] as "Software entities (classes, modules, functions, etc) should be open for extension, but closed for modification." OCP relates to the design smell of rigidity. During my weekly IPM yesterday, my mentor helped elaborate the concept by providing an example of where I followed the OCP and another scenario where the principal was violated. 

The definition of OCP itself seems to be a bit contradictory, however by seeing examples in my own code I was able to get a solid understanding of what the principal really meant! OCP allows programmers to anticipate change along an axis. By making certain design decisions you can make your program more receptive towards specific changes. 

{% highlight Ruby %}

def diagonal_major?(board, mark) #Initial
	board[0] == mark && board[4] == mark && board[8] == mark
end

def diagonal_major?(board, mark) #Enhanced
  count = 0
  for index in 0..board.size - 1
    count += 1 if (index % row_length + 1) == 0 and board[index] == mark
    true if count == row_length
  end
  false
end
	
{% endhighlight %}

One specification my mentor laid out was to have the option of having a four by four board in addition to a three by three board. This specification made me decide that my tic tac toe winning checks should be modified to work for any board size. My initial iteration was fixed for a board size of three by three. By making this improvement my program should be closed for modification in regards to square boards of any size. While this modification would still need modification to work for connect four, it should work for any size of tic tac toe board! 

One situation where I had not anticipated the need for OCP was in regards to how I designed the Players of the board. My AI utilizes a function called `smart_move(args)` whereas my human player has a function called `human_move`. In the case that additional types of Players were added to my specifications, my runtime loop would require modification. 

[PPP][ppp] notes "Fool me once..." and notes that "When a change occurs, we implement the abstractions that protect us from future changes of that kind. In short, we take the first bullet, and then we make sure we are protected from any more bullets coming from that gun." If additional Player specifications are never added to the requirements of this project, applying OCP may not be necessary. For example, while working on a client, you may code certain aspects of the code not expecting them to change. As the project grows and new specifications are added, it will become more clear which entities should have OCP applied and where it is not necessary. Per my example above, the board check that anticipates change of board size is a bit more complicated than the initial fixed size check. If my specification never extended beyond a three by three board the improvement would add needless complexity which itself is a design smell!  

[ppp]: http://www.amazon.com/Software-Development-Principles-Patterns-Practices/dp/0135974445