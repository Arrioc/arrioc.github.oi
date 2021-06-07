![myCatASCII](https://user-images.githubusercontent.com/73560858/120911070-355f7b80-c652-11eb-96c7-309bdd3cd158.png)


# Hello and Welcome! This ePortfolio features a program iteration with more to come! 
This ePortfolio is about a program I created in my CS 340 Client-Server course. I chose to enhance this project because it utilizes a culmination of concepts from past courses that best reflect my skills in software engineering, algorithms and thier data structures, and databases. 

## The following is a code review...
that explains the chosen project and its code, analyzes the code for flaws, and decides on a plan for enhancement. 
The video is 41m. I'd like to edit this down soon. It's a bit of a rough second draft. 😅


Watch [Arrioc's Video!](https://www.youtube.com/watch?v=wDXqfWe2RQw) 

## The Plan
My plan for software engineering and design is to improve the software by creating more readable output, more user-friendly input, and a well-rounded 'update' module for the API which will help to deliver better value. I will also remove unused code, improve commenting and try to fix any bugs.

The plan for algorithms and data structures is to add to the complexity of the artifact by creating new algorithms. These algorithms will allow for internal and API module field deletion, internal document retrieval and a menu that allows users to select program services to run.

My plan for database enhancement is to utilize more advanced administrative methods to investigate and apply performance tuning on the database, with the end-goal of improving database efficiency by speeding up its reads and writes.



# Software Design & Engineering

* ## The artifact
  * The artifact I chose for enhancement is a RESTful webservice stack with an industry-standard interface that I created in my CS 340 Client-Server course six months ago. This program can perform queries and aggregations, reporting on documents in the database in numerous ways. It can also create, read, update, and delete (CRUD) documents for a stock broking company both internally and externally through a web service that utilizes the RESTful API.
 
* ## Artifact Rationale
  * I chose to enhance this project because it is a culmination of my understanding of past courses and best reflects my skills in software design and engineering in that it demonstrates my knowledge and competence in solving real world problems that deliver value. What is more, it is all my own in that it does not lean on someone else’s ability to design solutions to a problem.

* ## Knowledge Acquisition
  * The MongoDB database shows that I understand how to import and manage a distributed database using appropriate MongoDB statements, such as creating simple and complex indexes. This is an important skill to have because “NoSQL databases like MongoDB are emerging as the next big thing” (Sriparasa & D’mello, 2018, p. 136). This NoSQL database is fast, flexible, and scalable, and it provides tons of features that do not sacrifice speed (Chodorow, 2013, pp. 3-5). 

  * Both the internal and API modules show that I understand how to connect to the database and carry out simple and complex functions using the appropriate JavaScript Object Notation (JSON), a widely popular data interchange format (Sriparasa & D’mello, 2018, p. 6). This is a critical skill to have because JSON is the go-to language for data interchange today (Sriparasa & D’mello, 2018, pp. 6-7). The internal and API modules show that I understand how apply CRUD functions for MongoDB database documents, perform queries and aggregations, test the code, find solutions to problems using branches and loops, and perform exception handling. The API modules show that I understand how to create and test uniform resource identifiers (URI's) and locators (URL’s), and implement the use of a basic RESTful web service using a language-specific web service framework like Bottle to rout paths and perform connections. 

* ## Collaboration
  * This artifact is the product of collaboration. Although I did create the program on my own, it took collaborating with peers, tutors, and instructors to for me to succeed. My peers and I in both the course’s discussion forum, and in SNHU’s Slack Chat for coders, helped each other progress. Tutors both from Slack Chat and our institution’s academic services assisted in helping me debug code and learn different ways to implement my ideas. Instructors have given me regular feedback which has helped to broaden my understanding. The artifact also has the collaborative coding help site, Stack Overflow, to thank for its success.

* ## Developing Solutions
  * I met the planned objectives for creating more readable output, more user-friendly input, and a well-rounded update module for the API which helps to deliver better value. The artifact now has improved readability by integrating JSON code into specific inputs and outputs, for any module that outputs data to the user. The artifact now has friendlier user input capability, by removing code that required the user to preformat their own inputs and injecting code that preformats the inputs for them using the JSON and Pymongo language. This allowed me to remove "bad formatting" error catch blocks. The API update module now better reflects the industry specific goal for update functionality by allowing the user to update any field in a specified document (not just the “volumes” field), or insert a new one, using the simple but effective solution of adding a variable to the CURL which is extracted and queried. I also added needed annotation comments to every module and fix a bug for the API modules that would reprint the last response posted in the terminal as you exited. 

* ## Reflecting on the Process
  * As I worked to improve the API’s update program to accept any user field, after many failures, I began examining other examples of ways in which CURLS can be made. By observing in the “stockReport” module that I was able to take a key variable “array” to input its value, an idea occurred to me. I could simply create a new “key” variable for the CURL whose value would be the embedded key and value which I wanted to extract. I applied the idea to the module, and it worked. 
  
  * As I worked to remove user formatting issues such as having the user input data in JSON or with quotes, I was faced with the challenge of needing to know exactly what the JSON utility, “loads”, and “dumps” were doing to the input code. I researched “loads” and “dumps” to refresh my memory and found a great site that explains specifically what they do. Loads turns strings into JSON objects, and dumps turns JSON objects into strings (Educative, Inc., 2021). Understanding “loads” and “dumps” allowed me format input for the user, simplifying thier tasks. This understanding also helped me my next task- fixing output readability.
  
  * I almost gave up creating more readable output because sites like StackOverflow repeatedly siad it was not possible (Stack Exchange Inc, 2015). Help-site opinions are not always accurate, sometimes it helps to ignore opinions dive deeper. For me, it helped to study an old exercise (a “timestamp” module) whose output to the terminal looked ideal. The code used “loads” before printing, and then use “dumps” along with some commands inside the print statement. Inside the print parentheses, after the string or variable to print, one can write “indent=4, default=json_util.default.” This indents the data, making it more exposed and orderly. I then applied this knowledge to every module that outputs data, including the API (for future developers). I then made a post about my discovery to StackOverflow, for future questioners like myself. Since then, someone edited it to look nicer using color coding and highlighting, which I was surprised to see.


  * **References**
   * ###### Chodorow, K. (2013). Mongo DB: The definitive guide (2nd ed.). O’Reilly Media, Inc. https://www.oreilly.com/library/view/mongodb-the-definitive/9781449344795/

   * ###### Sriparasa, S., & D’mello, B. (2018). JavaScript and JSON essentials : Build light weight, scalable, and faster web applications with the power of JSON (2nd ed.). Packt Publishing. https://search-ebscohost-com.ezproxy.snhu.edu/login.aspx?direct=true&db=nlebk&AN=1801025&site=eds-live&scope=site

   * ###### Educative, Inc. (2021). What is the difference between json.loads() and json.dumps()? https://www.educative.io/edpresso/what-is-the-difference-between-jsonloads-and-jsondumps

   * ###### Stack Exchange Inc. (2015, December 28). Pretty printing of output in Pymongo. StackOverflow. Retrieved May 22, 2021, from https://stackoverflow.com/questions/34493535/pretty-printing-of-output-in-pymongo


