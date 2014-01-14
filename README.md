##
##
##
##

Instructions:
-------------
To start off let's talk about how this library works. In order to bind data to an object from a result set 
we require you to name your columns in your database exactly the same as your properties in your object. 
The library will not work if you don't perform this crucial step first. Next let's talk about decorating 
your properties with some annotations. The following annotations are available, @PrimaryKy and @DataParameter

Step 1.) Name your properties the exact same name as they are in the DB.

Step 2.) Decorate your properties with the following annotations. 
     @PrimaryKey - Obviously represents the primary key of the object you are storing in your db.
     @DataParameter - Is any other field type in your database that relates to your object.

Step 3.) Add an interface that contains strings. The strings should be set to the names of the stored procedures you want to call.

An example class is below
------------------------- 
 
	public class User {
		@PrimaryKey
		@DataParameter
		public int UserID;
 
		@DataParameter
		public String AuthToken;
 
		@DataParameter
		public String Email;
 
		@DataParameter
		public String FirstName;
 
		@DataParameter
		public String LastName;
 
		@DataParameter
		public byte[] Password;
 
		@DataParameter
		public byte[] Salt;
 
		@DataParameter
		public String Username;
	
		public User() {	}
 
		public interface Procedures {
			String User_Add = "User_Add";
			String User_Get_All = "User_Get_All";
			String User_Get_By_UserID = "User_Get_By_UserID";
			String User_Remove_By_UserID = "User_Remove_By_UserID";
		}
	}


In order to use the library instantiate a new DB object like so.

     DB db = new DB(server, database, username, password);
     -----------------------------------------------------
or

     DB db = new DB(server, database, username, password, "3306");
     -------------------------------------------------------------


In order to make a call on a stored procedure and have it cast into a result set, do the following.

     List<User> users = db.ReadCollection(User.class, User.Procedures.User_Get_All);
     -------------------------------------------------------------------------------





For any questions, feel free to email me at steven@m-mb.com

Thanks!







