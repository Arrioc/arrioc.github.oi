![myCatASCIIsmaller](https://user-images.githubusercontent.com/73560858/120907519-27006800-c630-11eb-8353-74487520dd3c.jpg)


# Hello and Welcome! This ePortfolio features a program iteration with more to come! 
This ePortfolio is about a program I created in my CS 340 Client-Server course. I chose this project because it utilizes a culmination of concepts from past courses that best reflect my skills in software design/engineering, algorithms and thier data structures, and databases. In other words, it best demonstrates my knowledge and competence in solving real world problems that deliver value. 

Whats more, it's all my own! 


## The following is a code review...
that explains the chosen project and its code, analyzes the code for flaws, and decides on a plan for enhancement. 
The video is 41m. I'd like to edit this down soon. It's a bit of a rough second draft. 😅


Watch [Arrioc's Video!](https://www.youtube.com/watch?v=wDXqfWe2RQw) 


The initial plan is to improve the design by enhancing existing code, add to the complexity of the design by adding new features, and enhancing the database through performance-tuning. 


# Enhancement One: Software Design & Engineering

## The artifact
######    The artifact I chose for enhancement is a RESTful webservice stack with an industry-standard interface that I created in my CS 340 Client-Server course six months ago. This program can perform queries and aggregations, reporting on documents in the database in numerous ways. It can also create, read, update, and delete (CRUD) documents for a stock broking company both internally and externally through a web service that utilizes the RESTful API.
Artifact Rationale
    I chose this project because it is a culmination of my understanding of past courses and best reflects my skills in software design and engineering in that it demonstrates my knowledge and competence in solving real world problems that deliver value. What is more, it is all my own in that it does not lean on someone else’s ability to design solutions to a problem.

## Knowledge Acquisition
    The MongoDB database shows that I understand how to import and manage a distributed database using appropriate MongoDB statements, such as creating simple and complex indexes. This is an important skill to have because “NoSQL databases like MongoDB are emerging as the next big thing” (Sriparasa & D’mello, 2018, p. 136). This NoSQL database is fast, flexible, and scalable, and it provides tons of features that do not sacrifice speed (Chodorow, 2013, pp. 3-5). 
    Both the internal and API modules show that I understand how to connect to the database and carry out simple and complex functions using the appropriate JavaScript Object Notation (JSON), a widely popular data interchange format (Sriparasa & D’mello, 2018, p. 6). This is a critical skill to have because JSON is the go-to language for data interchange today (Sriparasa & D’mello, 2018, pp. 6-7). The internal and API modules show that I understand how apply CRUD functions for MongoDB database documents, perform queries and aggregations, test the code, find solutions to problems using branches and loops, and perform exception handling. The API modules show that I understand how to create and test uniform resource identifiers (URL’s) and implement the use of a basic RESTful web service using a language-specific web service framework like Bottle to rout paths and perform connections. 

## Collaboration
  This artifact is the product of collaboration. Although I did create the program on my own, it took collaborating with peers, tutors, and instructors to for me to succeed. My peers and I in both the course’s discussion forum, and in SNHU’s Slack Chat for coders, helped each other progress. Tutors both from Slack Chat and our institution’s academic services assisted in helping me debug code and learn different ways to implement my ideas. Multiple instructors have given me regular feedback and thus have assisted in both the program’s design and functionality. The artifact also has the collaborative coding help site, Stack Overflow, to thank for its success.

## Developing Solutions
  I met the planned objectives for creating more readable output, more user-friendly input, and a well-rounded update module for the API which helps to deliver better value. The artifact now has improved readability by integrating JSON code into specific inputs and outputs, for any module that outputs data to the user. The artifact now has friendlier user input capability, by removing code that required the user to preformat their own inputs and injecting code that preformats the inputs for them using the JSON and Pymongo language. This allowed me to remove error blocks for “bad formatting” type responses to the user. The API update module now better reflects the industry specific goal for update functionality by allowing the user to update any field in a specified document (not just the “volumes” field), or insert a new one, using the simple but effective solution of adding a variable to the CURL which is extracted and queried. I added some needed annotation comments to every module and fix a bug for the API modules that would reprint the last response posted in the terminal as you exited. 

## Reflecting on the Process
  As I worked to improve the API’s update program to accept any user field, after many failures, I began examining other examples of ways in which CURLS can be made. By observing in the “stockReport” module that I was able to take a key variable “array” to input its value, an idea occurred to me. I could simply create a new “key” variable for the CURL whose value would be the embedded key and value which I wanted to extract. I applied the idea to the module, and it worked. Although I tried several other methods of extracting the data from the CURL, this is the best way I could find so far, but I do not know if there is a more optimal way. 
  
  As I worked to remove user formatting issues such as having the user input data in JSON or with quotes, I was faced with the challenge of needing to know exactly what the JSON utility, “loads”, and “dumps” were doing to the input code. I researched the “loads” and “dumps” extensions to refresh my memory and found a great site that explains specifically what JSON “loads” and “dumps” do, with executable examples that let you edit the given code. I learned that “loads” turns strings into JSON objects, and that “dumps” turns JSON objects into strings (Educative, Inc., 2021). I felt this was perfect for what I wanted. I tinkered with the interactive executable examples and tested a sample of my code in it, and it showed me what “loads” and “dumps” was doing with my code. I now understand “loads” and “dumps” much better, and this understanding allowed me to carry out my next task- fixing user output readability. I also had to do a little refresher on different ways to apply and update a dictionary for the ‘stocks_create” file, but this was simple enough to figure out.
  
  I almost gave up creating more readable output because sites like Stack Overflow stated that it was not possible (Stack Exchange Inc, 2015). It helped to study an old project I had made, a “timestamp” module that interacted with the API. Its output looked like what I wanted. In studying this code, I learned that to carry out my goal I first need to use “loads” before it was printed, and then use “dumps” along with some commands within the print statement. Most of my code already used “loads” before printing, but that you can use “loads” in either the print statement (or return) or prior to printing. Inside the print parentheses, but after my output variable or string to print, I put “indent=4, default=json_util.default”. That indents the data, making it more readable. I then applied this technique to every program that outputs data. I was curious and applied it to the API modules as well. Even though an API would typically have a front-end handling readability, I felt future developers might appreciate it. I then made a post to Stack Overflow for future questioners like myself. Since then, someone edited it to look nicer using color coding and highlighting, which I was surprised to see.
 
 
## References

Chodorow, K. (2013). Mongo DB: The definitive guide (2nd ed.). O’Reilly Media, Inc. https://www.oreilly.com/library/view/mongodb-the-definitive/9781449344795/
Sriparasa, S., & D’mello, B. (2018). JavaScript and JSON essentials : Build light weight, scalable, and faster web applications with the power of JSON (2nd ed.). Packt Publishing. https://search-ebscohost-com.ezproxy.snhu.edu/login.aspx?direct=true&db=nlebk&AN=1801025&site=eds-live&scope=site

Educative, Inc. (2021). What is the difference between json.loads() and json.dumps()? https://www.educative.io/edpresso/what-is-the-difference-between-jsonloads-and-jsondumps

Stack Exchange Inc. (2015, December 28). Pretty printing of output in Pymongo. StackOverflow. Retrieved May 22, 2021, from
https://stackoverflow.com/questions/34493535/pretty-printing-of-output-in-pymongo


