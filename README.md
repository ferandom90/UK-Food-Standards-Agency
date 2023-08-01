# nosql-UK Food Standards Agency

NoSQL_setup_starter:
The code performs various analyses on a MongoDB database named uk_food that contains information about food establishments in the UK. Let's go through each part and analyze the code.

Part 1: Importing Dependencies
The code imports the necessary dependencies for working with MongoDB (pymongo), pretty printing (pprint), and data manipulation (pandas).

Part 2: Database Connection and Collection Selection
The code establishes a connection to the MongoDB server running on the default port 27017 using the MongoClient class. It then assigns the uk_food database to the db variable. The available collections in the database are printed using db.list_collection_names(), and the "establishments" collection is assigned to the establishments variable.

Part 3: Exploratory Analysis
1. Establishments with a Hygiene Score of 20

The code sets a filter to find establishments with a hygiene score of 20 (filter = {"scores.Hygiene": 20}). It then performs the following actions:

It retrieves and prints all the establishments that match the filter using establishments.find(filter) and pprint(result).
It counts the number of documents that match the filter using establishments.count_documents(filter) and prints the result.
It retrieves the first document that matches the filter using establishments.find_one(filter) and prints the result using pprint().
It converts the query result into a Pandas DataFrame using a list comprehension and pd.DataFrame().
It prints the number of rows in the DataFrame using data_frame.shape[0].
It displays the first 10 rows of the DataFrame using pprint(data_frame.head(10)).
2. Establishments in London with RatingValue >= 4

The code sets a filter to find establishments in London with a RatingValue greater than or equal to 4. It performs similar operations as in the previous analysis, including printing the establishments, counting the documents, retrieving the first document, converting the result to a DataFrame, printing the number of rows in the DataFrame, and displaying the first 10 rows.

3. Top 5 Establishments with RatingValue 5, Sorted by Lowest Hygiene Score (Near "Penang Flavours")

The code defines search parameters for the establishment name ("Penang Flavours") and geographical coordinates (latitude: 51.490142, longitude: 0.08384). It performs the following steps:

It constructs a query to find establishments within a small latitude and longitude range around the specified coordinates, with a RatingValue of 5.
The query results are sorted by the hygiene score in ascending order and limited to the top 5 establishments using sort() and limit().
The code then retrieves and prints the establishments, similar to the previous analyses.
It converts the query result to a DataFrame and prints it using pprint().
4. Number of Establishments with Hygiene Score 0 in Each Local Authority Area

The code creates a MongoDB aggregation pipeline to perform the following operations:

Match establishments with a hygiene score of 0.
Group the matched establishments by Local Authority.
Sort the groups in descending order based on the count of establishments.
It executes the aggregation pipeline using establishments.aggregate(pipeline).
The code prints the results and the first 10 results separately.
It converts the aggregation result to a DataFrame and prints the number of rows and the first 10 rows.
Overall, the code connects to a MongoDB database, performs various queries using filters, retrieves results, and converts them to Pandas DataFrames for further analysis and display.





NoSQL_analysis_starter:
The code is performing an analysis and update operations on a MongoDB database named uk_food with a collection named establishments. Here is a breakdown of the code:

Part 1: Database and Jupyter Notebook Set Up

The code begins by importing the necessary dependencies, including MongoClient from pymongo and pprint from pprint.
An instance of MongoClient is created, connecting to the MongoDB server running on the default port 27017.
The available databases are listed using list_database_names(), and the result is printed using pprint.
The uk_food database is assigned to the variable db.
The collections in the uk_food database are listed using list_collection_names(), and the result is printed using pprint.
The collections in the uk_food database are listed again to verify.
A document from the establishments collection is retrieved using find_one(), and the result is printed using pprint.
The establishments collection is assigned to the variable establishments.
Part 2: Update the Database

A dictionary named restaurant_data is created, representing information about a new restaurant.
The new restaurant document is inserted into the establishments collection using insert_one(), and the inserted document's ID is printed.
BusinessTypeID for "Restaurant/Cafe/Canteen" is fetched from the establishments collection using find(), returning only the relevant fields.
The new restaurant document is updated with the correct BusinessTypeID using update_one().
The number of documents with LocalAuthorityName as "Dover" is counted using count_documents().
All documents where LocalAuthorityName is "Dover" are deleted using delete_many(), and the number of deleted documents is printed.
It checks if any remaining documents include LocalAuthorityName as "Dover" and prints a message if any are found.
Another document from the establishments collection is printed using find_one().
The data types of geocode.longitude, geocode.latitude, and RatingValue fields are converted from strings to numbers using update_many() and $toDouble or $toInt operators.
The non-rating values ("AwaitingInspection", "Awaiting Inspection", "AwaitingPublication", "Pass", "Exempt") in the RatingValue field are set to None using update_many().
The coordinates and rating value from documents where they exist are retrieved and printed using find() and pprint.
The code primarily focuses on database operations like connecting to the database, inserting, updating, deleting documents, and performing data type conversions.

