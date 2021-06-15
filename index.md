![myCatASCII](https://user-images.githubusercontent.com/73560858/120911070-355f7b80-c652-11eb-96c7-309bdd3cd158.png)
###### ASCII Art by Jessica Kilbourne. 

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

# The Artifact
  * The artifact I chose for enhancement is a representational state transfer (RESTful) webservice stack with an industry-standard interface that I created in my CS 340 Client-Server course six months ago. This program can perform queries and aggregations, reporting on documents in the database in numerous ways. It can also create, read, update, and delete (CRUD) documents for a stock broking company both internally and externally through a web service that utilizes the RESTful application programming interface (API).
 
# Artifact Rationale
  * I chose to enhance this project because it utilizes a culmination of concepts from past courses that best reflect my skills in software engineering, algorithms and thier data structures, and databases, in that it demonstrates my knowledge and competence in solving real world problems that deliver value. There are a dozen different algorithms, each within their own portable and reusable module, and they all interact with the MongoDB database. Perfect for showing off my skills in design, implementing algorithms and displaying my database prowess. What is more, it is all my own in that it does not lean on someone else’s ability to design solutions to the problem.

# Collaboration
  * This artifact is the product of collaboration. Although I did create the program on my own, it took collaborating with peers, tutors, and instructors to for me to succeed. My peers and I in both the course’s discussion forum, and in SNHU’s Slack Chat for coders, helped each other progress. Tutors both from Slack Chat and our institution’s academic services assisted in helping me debug code and learn different ways to implement my ideas. Instructor feedback has broadened my understanding, and that has contributed to my work. The artifact also has the collaborative coding help site, Stack Overflow, to thank for its success.

# Software Design & Engineering

* ## Knowledge Acquisition
  * The MongoDB database shows that I understand how to import and manage a distributed database using appropriate MongoDB statements, such as creating simple and complex indexes. This is an important skill to have because “NoSQL databases like MongoDB are emerging as the next big thing” (Sriparasa & D’mello, 2018, p. 136). This NoSQL database is fast, flexible, and scalable, and it provides tons of features that do not sacrifice speed (Chodorow, 2013, pp. 3-5). 

  * Both the internal and API modules show that I understand how to connect to the database and carry out simple and complex functions using the appropriate JavaScript Object Notation (JSON), a widely popular data interchange format (Sriparasa & D’mello, 2018, p. 6). This is a critical skill to have because JSON is the go-to language for data interchange today (Sriparasa & D’mello, 2018, pp. 6-7). The internal and API modules show that I understand how apply CRUD functions for MongoDB database documents, perform queries and aggregations, test the code, find solutions to problems using branches and loops, and perform exception handling. The API modules show that I understand how to create and test uniform resource identifiers (URI's) and locators (URL’s), and implement the use of a basic RESTful web service using a language-specific web service framework like Bottle to rout paths and perform connections. 

* ## Developing Solutions
  * I met the planned objectives for creating more readable output, more user-friendly input, and a well-rounded update module for the API which helps to deliver better value. The artifact now has improved readability by integrating JSON code into specific inputs and outputs, for any module that outputs data to the user. The artifact now has friendlier user input capability for all modules, by removing code that required the user to preformat their own inputs and injecting code that preformats the inputs for them using the JSON and Pymongo language. This allowed me to remove "bad formatting" error catch blocks. The API update module now better reflects the industry specific goal for update functionality by allowing the user to update any field in a specified document (not just the “volumes” field), or insert a new one, using the simple but effective solution of adding a variable to the CURL which is extracted and queried. I also added needed annotation comments to every module and fixed a bug for the API modules that would reprint the last response posted in the terminal as one exits. 

  * ## Better User Input Code & Commenting:
 
  * ```python
    import json
    from bson import json_util
    from pymongo import MongoClient, errors
    from bson.json_util import dumps, loads

    connection = MongoClient('localhost', 27017)
    db = connection['market']
    collection = db['stocks']

    # This method returns 'false' and a message for when 
    # document creation wasn't successful

    def update_document(query, newMod):
      try:
        myUpdateResult = collection.update_one(query, newMod)
        return myUpdateResult
      except errors.DuplicateKeyError as e:
        print("Duplicated key error", e)               
        return False                                    
      except WriteError as we:
        print("MongoDB returned error message", we)
        return False
      except WriteConcernError as wce:
        print("MongoDB returned error message", wce)
        return False
      except PyMongoError as pm:
        print("MongoDB returned error message", pm)
        abort(400, str(pm))
        return
    
    # This method accepts input for a ticker. If the ticker doesnt 
    # exist it exits, else it takes input for a key and value, and
    # preformats them. It then sends this data to the update 
    # function.On return, it reports on whether the update worked.

    def modify_main():

      #request ticker data for query
      print('Please enter capitolized Ticker name')

      #store variable for query
      newQuery = (raw_input())                          
      #format user input                                
      myQuery = loads("{\"Ticker\" : \""+newQuery+"\"}")
      #check for document existance, exit if none
      if (not collection.find_one(myQuery)):
        print("Document not found.")            

      #else continue...
      else:
        #store field input for modify_doc                  
        print('Please enter field name')                    
        key = (raw_input())
        print('Please enter field value')
        value = (raw_input())
        #check whether string or number, format accordingly
        if (value == int or float and not str):           
          modify = loads("{\""+key+"\" : "+value+"}")
        else:                                             
          modify = loads("{\""+key+"\" : \""+value+"\"}")

        newUpdate = {"$set" : modify}                         

        #update execution with query and modification
        myUpdateResult = update_document(myQuery, newUpdate)

        #if file was updated
        if (myUpdateResult.modified_count == 1):
          # print raw result & update results
          print(dumps(myUpdateResult.raw_result))
          print("Document updated!")
        #if file is not updated
        else:
          #print raw result & update result
          print(dumps(myUpdateResult.raw_result))
          print("File was not modified, possibly because the modification already exists.")


    modify_main()
    ```
    
   * User Input Before Enhancement:
   * ![internal update before3](https://user-images.githubusercontent.com/73560858/121097947-dcfbbb80-c7c2-11eb-9189-6c3ce43830d9.png)
 
   * User Input After Enhancement:
   * ![internal update, after](https://user-images.githubusercontent.com/73560858/121097482-09630800-c7c2-11eb-936e-2f46bb8b08f4.png)

  * ## Better Readability Code: 
  * ```python
    import json
    from bson import json_util
    from pymongo import MongoClient, errors
    from bson.json_util import dumps
    from bottle import get, route, run, request, abort

    connection = MongoClient('localhost', 27017)
    db = connection['market']
    collection = db['stocks']

    # This method executes the aggregation pipeline, then reports
    # a portfolio on the top five shares with the given aggregation 
    # criteria.

    #aggregate Function
    def aggregate(aggreg): 
      try:
        myReadResult = collection.aggregate(aggreg)
        print(myReadResult)
        #if aggregation does not equal 'None'
        if (myReadResult != None):
          #convert to json and print                 
          print("Top five shares grouped by company, strength, 200-Day SMA.")
          print(dumps(myReadResult, indent=4, default=json_util.default)) 
        return
      except Exception as pm:
        print(dumps("MongoDB returned error message", pm))

    # This method extracts the CURLS's industry and sets up an
    # aggregation pipeline with it. The aggregation matches the industry 
    # and groups the top companies by thier relative strength index and 
    # the highest 200-Day SMA. It then sorts them by their highest strength
    # index. The method first reports an error if the industry doesnt exist, 
    # it then sends the aggregation to the 'aggregation' function.

    #URI for REST service
    @get('/stocks/api/v1.0/industryReport')
    def main_aggregate_API():

      #take value for query
      industry = request.json["Industry"]

      #aggregation filtering & projection criteria
      aggregationQ = [{"$match" : {"Industry" : {"$regex" : ".*"+industry+".*"}}}, {"$sort" : {"HighestStrength" : -1}},
                      {"$group" :  {"_id" : "$Company", "HighestStrength" : 
                       {"$max" : "$Relative Strength Index (14)"},"Highest200-DaySMA" : 
                       {"$max" : "$200-Day Simple Moving Average"}}},
                       {"$limit" : 5}]

      #if industry query doesnt exist, print error
      match = {"Industry" : {"$regex" : ".*"+industry+".*"}}
      if (collection.find(match).count() == 0):
        print("No Matches Found For:")
        print(dumps(match))
      #else send variables to aggregation function
      else: 
        myReadResult = aggregate(aggregationQ)

    if __name__ == '__main__':
        run(host='localhost', port=8080, debug=True)   
    ```
    
   * Readability Before:
   * ![indusrtyReport server result](https://user-images.githubusercontent.com/73560858/121100869-b50f5680-c7c8-11eb-89a1-6c413dab85a4.png)
   
   * Readability After:
   * ![terminal, server, APIindustryReport, fixed output- beautified](https://user-images.githubusercontent.com/73560858/121100215-59909900-c7c7-11eb-9e8b-4d0f4baf119b.png)
  
  * ## Improved API Update Code:
  * ```python
    import json
    from bson import json_util
    from bson.json_util import dumps
    from pymongo import MongoClient, errors
    from bottle import get, put, route, run, request, abort

    connection = MongoClient('localhost', 27017)
    db = connection['market']
    collection = db['stocks']

    # This method executes the update and returns results to 
    # the main program. If they ticker was modified, and the
    # new ticker already exists, duplicate key error is reported.

    #update funtion
    def update_document(query, newMod):
      try:
        myUpdateResult = collection.update_one(query, newMod)
        return myUpdateResult
      except errors.DuplicateKeyError as e:
        print("Duplicated key error", e)               
        return False  
      except errors.PyMongoError as pm:
        print("MongoDB returned error message", pm)
        abort(400, str(pm))
        return

    # This method takes a ticker and key from the users CURL.
    # It uses the ticker as the query parameter, and sets the 
    # key's value (which is a key and value) as the update parameter
    # and calls 'update_function'. Upon return, the result is checked 
    # and reports whether the document was updated, has already been 
    # modified, or is not found.

    #URI paths for REST service
    @put('/stocks/api/v1.0/updateStock')
    def main_update_API():
      #get ticker    
      ticker = request.params.get('ticker')
      myQuery = {"Ticker" : ticker}  
      #check for document existance, exit if none 
      if (not collection.find_one(myQuery)):
        print("Document not found.")

      #else continue...
      else:  
        #get key & value in json       
        modify = request.json["key-value"]  
        #set key and value to update
        newUpdate = {"$set" : modify}

        #pass query and update to update function
        myUpdateResult = update_document(myQuery, newUpdate)

        #if file was modified
        if (myUpdateResult.modified_count == 1):
          #print raw result & update result
          print(dumps(myUpdateResult.raw_result))
          print("Document updated!")
        #if file was not modified  
        else:
          #print raw result & update result
          print(dumps(myUpdateResult.raw_result))
          print("File was not modified. The modification already exists.")

    if __name__ == '__main__':
        run(host='localhost', port=8080, debug=True)  
    ```

   * Hard-Coded VS. Not Hard-Coded + CURLS Used:
   * ![APIupdate, before, after, curl](https://user-images.githubusercontent.com/73560858/121099782-7e384100-c7c6-11eb-955e-31cca216d171.png)
   
   * Database Before and After CURL:
   * ![APIupdate database before and after](https://user-images.githubusercontent.com/73560858/121099895-bfc8ec00-c7c6-11eb-95d4-724091db8373.png)

* ## Reflecting on the Process
  * As I worked to improve the API’s update program to accept any user field, after many failures, I began examining other examples of ways in which CURLS can be made. By observing in the “stockReport” module that I was able to take a key variable “array” to input its value, an idea occurred to me. I could simply create a new “key” variable for the CURL whose value would be the embedded key and value which I wanted to extract. I applied the idea to the module, and it worked. 
  
  * As I worked to remove user formatting issues such as having the user input data in JSON or with quotes, I was faced with the challenge of needing to know exactly what the JSON utility, “loads”, and “dumps” were doing to the input code. I researched “loads” and “dumps” to refresh my memory and found a great site that explains specifically what they do. Loads turns strings into JSON objects, and dumps turns JSON objects into strings (Educative, Inc., 2021). Understanding “loads” and “dumps” allowed me format input for the user, simplifying thier tasks. This understanding also helped me my next task- fixing output readability.
  
  * I almost gave up creating more readable output because sites like StackOverflow repeatedly siad it was not possible (Stack Exchange Inc, 2015). Help-site opinions are not always accurate. Sometimes it helps to ignore opinions and dive deeper. For me, it helped to study an old exercise (a “timestamp” module) whose output to the terminal looked ideal. The code used “loads” before printing, and then use “dumps” along with some commands inside the print statement. Inside the print parentheses, after the string or variable to print, one can write “indent=4, default=json_util.default.” This indents the data, making it more exposed and orderly. I then applied this knowledge to every module that outputs data, including the API (for future developers). I then made a post about my discovery to StackOverflow, for future questioners like myself. Since then, someone edited it to look nicer using color coding and highlighting, which I was surprised to see.


# Algorithms and Data Structures
* ## Knowledge Acquisition
  * This artifact showcases a diverse collection of skills and abilities in using algorithms and data structures to perform useful database manipulations that meet the client’s needs. The artifact makes use of dictionaries, arrays, methods, functions, calls, conditional branches, expressions, statements, returns, formatting, dot-notation, and input/output using a combination of the MongoDB, Pymongo and Bottle languages and commands. The API modules show that I understand how to create and test uniform resource identifiers (URI's) and locators (URL’s), and implement the use of a basic RESTful web service using a language-specific web service framework like Bottle to rout paths and perform connections.  

  * The “create” programs utilize dictionary data structures internally, but also externally by using the bottle framework for a web service. This design choice better synchronizes with MongoDB’s dictionary-based storage design because dictionaries utilize mapping that allows indices of (almost) any type (Downey, 2015, p. 103). Python dictionaries also use hashtables which search in constant time and are high performance in that they cut down search time considerably (Downey, 2015, pp. 205-207). Also present in the “APIstockReport” is the use of an array for a data structure, returning multiple documents to the user. The module “stocks_read2” utilizes a reverse lookup by finding existing industries (a value) and returning their dictionary key/values for tickers in an array (Downey, 2015, p. 106). 

  * Modules like “stocks_read” utilize methods, functions, and branches with and without conditional statements to solve a problem. These modules make use of a “main” method which take the input from a user and then use statements that format input (and possible projections) to conduct a search of the database using a query. After checking for formatting errors or whether the query exists, the main method calls an execution function in the module. This function carries out the search or conducts calculations (in the case of “stocks_read1”) using parameters. These modules often use MongoDB dot-notation shell methods like “.count()” to check for a criteria’s existence (using conditional branches) and then prints data from the execution function. The pointer then returns to main, and the program exits. 

  * Modules that “update” and “delete” are much the same in structure as the “read” modules but differ in that their main methods take returns from called functions and perform condition checks using Pymongo’s dot-notation. I find notation like “.raw_result” very handy because it can tell me if the changes made were really carried out on the database, and this might contradict my print statements which helps to point out flaws in the code. 

  * Some modules that search the database do a bit more than simply output documents. These use MongoDB commands to apply functionality. For example, the module “stocks_read1” performs calculations on all “50-Day Simple Moving Average” values, and “stocks_read2” will match all values for the key “industry”. Functions, such as the “APIindustryReport” and “stocks_read3” modules, provide a valuable service to the business through aggregation which allows them to analyze and crunch data in interesting ways (Chodorow, 2013, p. 127). These modules use MongoDB’s ability to calculate, match and project data combined with the ability to aggregate data (group, sort, skip, and limit data) to present the data in a more useful way (Chodorow, 2013, p. 127).

* ## Developing Solutions
  * I met the planned objectives for adding to the complexity of the artifact by creating modules whose algorithms allow for field deletion, internal document retrieval and menu execution. The artifact now has web-service and internal modules that let a user delete a field (a key and value) in a document by having the user specify a ticker for querying and a key for deletion using MongoDB’s “$unset” and “update_one”.  The artifact now has an internal module that implements a simple “read” algorithm which queries and presents documents to the user. Finally, the artifact now has a menu which utilizes “while” loops to present the user with choices between internal or web-based services (or to exit), and then presents a list of options to choose from for each service. Internal modules are executed using import lines, while the API modules uses “os.system” program calls. If the user enters invalid input, they will get a “try again” response.

  * ## Algorithm For Internal Document Retrieval:
  * ```python
    import json
    from bson import json_util
    from pymongo import MongoClient, errors
    from bson.json_util import dumps, loads

    connection = MongoClient('localhost', 27017)
    db = connection['market']                             
    collection = db['stocks']                     

    # This method executes the query and reports on 
    # whether no file was found, otherwise it outputs 
    # the document requested or reports any error.

    #read function
    def read_document(document):
      try:
        myReadResult = collection.find(document)
        #if specific query exists
        if (myReadResult.count() != 0):
          #convert to json and print
          print(dumps(myReadResult, indent=4, default=json_util.default)) 
        #if result found 0 matching files  
        elif (myReadResult.count() == 0):
          #return error message
          print("No File Found With That Criteria.")
        return
      except errors.PyMongoError as pm:
        print("MongoDB returned error message", pm)
        abort(400, str(pm))
        return

    # This method takes from the user a ticker 
    # string, preformats it, and then sends it to
    # the 'read_document' query function.

    def read_main():
      print('Please enter capitolized ticker name')
      #store variable for query                           
      try:
        newQuery = (raw_input())                          
        #format user input                                
        myQuery = loads("{\"Ticker\" : \""+newQuery+"\"}")

      #return error if badly formatted data  
      except ValueError:
        print("ValueError: wrongly formatted doc!")
        return "Error occured"      
      except TypeError:
        print("ValueError: wrongly formatted doc!")
        return "Error occured"

      #send to read funtion
      myReadResult = read_document(myQuery)

    read_main()
    ```
  * ## Algorithm For Internal Field Deletion:
  * ```python
    import json
    from bson import json_util
    from bson.json_util import dumps, loads
    from pymongo import MongoClient, errors

    connection = MongoClient('localhost', 27017)
    db = connection['market']
    collection = db['stocks']

    # This method queries using the query parameter and executes deletion
    # on the field using the field parameter, then returns results to main.

    def delete_field(query, newFdel):
      try:
        myDeleteResult = collection.update_one(query, newFdel)
        return myDeleteResult
      except PyMongoError as pm:
        print("MongoDB returned error message", pm)
        abort(400, str(pm))
        return

    # This method takes user ticker input, and checks if it exists.  
    # If the ticker doesnt exist its reported and the program quits.
    # If the ticker exists a field name is requested, stored and 
    # formatted before being sent to the 'delete_field' funtion, 
    # and then reports on the results sent back from the funtion.

    def del_field_main():

      #request ticker data for query
      print('Please enter capitolized Ticker for the document to be modified.')

      #store variable for query
      newQuery = (raw_input()) 

      #format user input                                
      myQuery = loads("{\"Ticker\" : \""+newQuery+"\"}")

      #if query found no such ticker, report
      if (collection.find_one(myQuery) == None):
        print("Document not found.")

      #else continue...
      else:                                                              
        print('Please enter field to be removed with initial letter capitolized')

        #store field for deletion
        key = (raw_input())
        #format & load json for given field     
        deleteForm = "{\""+key+"\" : \"\"}"  
        removeField = loads(deleteForm)

        #store unset field to be removed 
        newFieldDel = {"$unset" : removeField}

        #send query & unset field to 'delete_field' function
        myDeleteResult = delete_field(myQuery, newFieldDel)


        #if modify count is 1
        if (myDeleteResult.modified_count == 1):
          #show confirmation results
          print(dumps(myDeleteResult.raw_result))
          print("Document field has been removed.")
        else:
          #show non-confirmation results
          print(dumps(myDeleteResult.raw_result))
          print("Document's field could not be found and may have already been removed.")

    del_field_main()   
    ```

  * ## Algorithm For API Field Deletion:
  * ```python
    import json
    from bson import json_util
    from pymongo import MongoClient, errors
    from bson.json_util import dumps
    from bottle import get, put, route, run, request, abort

    connection = MongoClient('localhost', 27017)
    db = connection['market']
    collection = db['stocks']

    # This method queries using the query parameter and executes deletion
    # on the field using the field parameter, then returns results to main.

    #delete field function
    def APIdelete_field(query, newFdel):
      try:
        myDeleteResult = collection.update_one(query, newFdel)
        return myDeleteResult
      except PyMongoError as pm:
        print("MongoDB returned error message", pm)
        abort(400, str(pm))
        return


    # This method takes the ticker from the CURL, and checks its existance.  
    # If the ticker doesnt exist its reported and the program quits.
    # If the ticker exists the field name is requested & stored in an 
    # "unset" statement before being sent to the 'delete_field' funtion. 
    # The method then reports on the results sent back from the funtion.

    #stocks_del_field:
    @put('/stocks/api/v1.0/delField')
    def main_del_field_API():

      #get ticker, store as json variable    
      ticker = request.params.get('ticker')
      myQuery = {"Ticker" : ticker}

      #if query found no such ticker, report
      if (collection.find_one(myQuery) == None):
        print("Document not found.")

      #else continue...
      else:                                                              
        #get key & store          
        key = request.json["Key"]

        #store unset field to be removed 
        newFieldDel = {"$unset" : key}

        #send query & unset field to 'delete_field' function
        myDeleteResult = APIdelete_field(myQuery, newFieldDel)

        #if modify count is 1
        if (myDeleteResult.modified_count == 1):
          #show confirmation results
          print(dumps(myDeleteResult.raw_result))
          print("Document field had been removed.")
        else:
          #show non-confirmation results
          print(dumps(myDeleteResult.raw_result))
          print("Document's field could not be found and may have already been removed.")


    if __name__ == '__main__':
        run(host='localhost', port=8080, debug=True) 

    ```

  * ## Algorithm For The Menu:
  * ```python
    import os

    # This method provides an initial menu that 
    # allows the user to chose between internal 
    # and web based services.

    def main_menu():
      reply = True
      print('Welcome to Kilbourne Financial\'s Stock Market Services. \nPlease select from the following:')
      #let user chooses from two types of services
      while reply:
        print("""
        1 Internal services
        2 Web services
        3 Exit """)

        reply = raw_input()

        if (reply == '1'):
          print("You chose internal services")
          internal()
        elif (reply == '2'):
          print("You chose web services")
          webService()
        elif (reply == '3'):
          print('Goodbye, have a great day!') 
          reply = False
        else:
          print('Does not compute! Try agian.')

    # This method provides services through the internal service
    # by taking a selection from the user and then executing 
    # the chosen module. When finished we return to the main menu

    def internal():
      select = True
      print('Welcome to internal services. \nPlease choose from the following:')
      #let user chose from different internal services
      while select:
        print("""
        1 Create a new stock document
        2 Update a document
        3 Delete a document
        4 Delete a document's field
        5 Find a document
        6 Report on 50-Day Simple Moving Average
        7 Get an industry's ticker symbol list
        8 Report on a sector's total oustanding shares
        9 Exit to main menu
        """)

        select = raw_input()

        if (select == '1'):
          print("You chose create a stock document")
          from stocks_create import create_main
        elif (select == '2'):
          print("You chose update document")
          from stocks_update import modify_main
        elif (select == '3'):
          print("You chose delete doument")
          from stocks_delete import delete_main
        elif (select == '4'):
          print("You chose delete document field")
          from stocks_deleteField import del_field_main
        elif (select == '5'):
          print("You chose find document")
          from stocks_read import read_main
        elif (select == '6'):
          print("You chose report 50-Day SMA")
          from stocks_read1 import read1_main
        elif (select == '7'):
          print("You chose Get industry ticker list")
          from stocks_read2 import read2_main
        elif (select == '8'):
          print("You chose report on a sector's total oustanding shares")
          from stocks_read3 import read3_main
        elif (select == '9'):
          print('Exiting') 
          select = False
        else:
          print('Does not compute! Try again')

    # This method provides services through the web service
    # by taking a selection from the user and then executing 
    # the chosen module

    def webService():

      select = True
      print('Welcome to internal services. \nPlease choose from the following:')
      #let user chose from different internal services
      while select:
        print("""
        1 Create a new stock document
        2 Update a document
        3 Delete a document
        4 Delete a document's field
        5 Find a document
        6 Find multiple documents
        7 Create industry report
        8 Exit to main menu
        """)

        select = raw_input()

        if (select == '1'):
          print("You chose create a stock document")
          os.system("python APIcreate.py")
        elif (select == '2'):
          print("You chose update document")
          os.system("python APIupdate.py")
        elif (select == '3'):
          print("You chose delete doument")
          os.system("python APIdelete.py")
        elif (select == '4'):
          print("You chose delete document field")
          os.system("python APIdeleteField.py")
        elif (select == '5'):
          print("You chose find document")
          os.system("python APIread.py")
        elif (select == '6'):
          print("You chose find multiple documents")
          os.system("python APIstockReport.py")
        elif (select == '7'):
          print("You chose create industry report")
          os.system("python APIindustryReport.py")
        elif (select == '8'):
          print('Exiting') 
          select = False
        else:
          print('Does not compute! Try agian.')


    main_menu()
    ```

* ## Reflecting on the Process
  * The read module was simple because I had done this sort of things many times before. The module that deletes fields was a new challenge. It helped to study my "delete" and "update" module’s code. Browsing through what “delete_one” can do in the online MongoDB documentation, I saw that this only applied to whole objects like documents. This reassured me that what I wanted to do was modify the document using “update_one”. I refreshed myself on MongoDB’s “$set” which resides in my update module. It updates existing keys or creates new ones. Realizing that I want the opposite of this, I began browsing through my MongoDB book and rediscovered “$unset” which does the opposite of “$set”. The end-product is a marriage between my “delete” and “update” module.

  * My biggest challenge for the menu was to figure out how to execute my modules from inside the menu. After much searching, I decided to ask for help. A tutor on Slack Chat hinted that one way I can execute my modules is by importing them but did not say how (they never do). I tried importing a module at the top of my code and I noticed that it would run my imported module before executing my menu. After that, I knew what to do: put the import lines with the menu options. The API modules are different, they can’t be started using the imports. After a bit of searching, I learned from a help site on Unix\Linux called NixCraft that I could import the “os” and use “os.system(“command”)” to execute my API’s (Vivec, 2013). I added these lines to my menu options for each API module. I also learned through trial and error that my internal Python files need to be in the directory with the REST API to have the menu fully functional.  


  * **References**
   * ###### Chodorow, K. (2013). Mongo DB: The definitive guide (2nd ed.). O’Reilly Media, Inc. https://www.oreilly.com/library/view/mongodb-the-definitive/9781449344795/

   * ###### Downey, A. (2015). Think python: How to think like a computer scientist (2nd ed.). Green Tea Press. https://greenteapress.com/thinkpython2/html/

   * ###### Educative, Inc. (2021). What is the difference between json.loads() and json.dumps()? https://www.educative.io/edpresso/what-is-the-difference-between-jsonloads-and-jsondumps

   * ###### Sriparasa, S., & D’mello, B. (2018). JavaScript and JSON essentials : Build light weight, scalable, and faster web applications with the power of JSON (2nd ed.). Packt Publishing. https://search-ebscohost-com.ezproxy.snhu.edu/login.aspx?direct=true&db=nlebk&AN=1801025&site=eds-live&scope=site

   * ###### Stack Exchange Inc. (2015, December 28). Pretty printing of output in Pymongo. StackOverflow. Retrieved May 22, 2021, from https://stackoverflow.com/questions/34493535/pretty-printing-of-output-in-pymongo

   * ###### Vivek, G. (2013, Dec 30). Python execute unix: Linux command examples. NixCraft. https://www.cyberciti.biz/faq/python-execute-unix-linux-command-examples/?__cf_chl_captcha_tk__=9bb51b5678d4ae41b922f8e73efc57d23d3559d6-1622059002-0-AcnFbvo4ZSPblHayQIbaQwyGXmPaaL2hezAfnWWm1oyv9ltGtxiXbF5AhKuRswuvjVBfALMQu4h4WOkB2Gzj3PVNgE0tWWENDj254bVYgM2k2gp6_NhPLulaHF6-U1bJb9GLVIcuK54JQlxcgo0TbKwApyZYToLtLN26q0UtOtsWIkufUP9j0VgHckL3ZuWM-TpmyVByMqZeWiD9Nbu8kNQxWViCJiRQ7LbRzGt9zr1D9D3HcMU-RFP3G-ywfC16dspUH_H5CQqUuyHYOzvhtJsd4h5uAQqJIQQsD5sNQekdioAlTzJexg_IbhygV3VDykNa73J5SWNEB1gquBxzYXBUDQsHOYRiBEuzfW1YhcUlmZ28yzKeFjLy4p3zHorQFmJmNndRj-5BoRulc_znV5Gj6-GiJuulchUfQUpkBy9FbVrk1yanKAatmhGu5YuVmbwHSoFYzMhc6HMnde3GH7UGPVwFF2Xg_SwQzhlviYW2eZITo7x6lSsu_iiL1gcTICEyQzKhdxJuwNFJjRotoO0LgDIiZONunnujhus_zkxRBHhN7jPP-qkGSvh_izK7khrtHw4oaS0Mxbc2NjT9THKk0iOpuXhnnJGGTL0hkIwB5ciqJlIAvmgiqvtGK7Ut-fjR0nydRM6DQl3e68cTFBbjNgXDSJDu64Kth7sjUgedo9bHIz3XW23_3b78xv5kRmyk53b2g5u1LLHBFmSDLC_0QhOWX6Zp2h3W9AbHT93l


