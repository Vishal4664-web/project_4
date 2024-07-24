import java.sql.*;

public class DatabaseExample {
  public static void main(String[] args) {
    // Load the JDBC driver
    try {
      Class.forName("com.mysql.cj.jdbc.Driver");
    } catch (ClassNotFoundException e) {
      System.out.println("Error loading JDBC driver: " + e.getMessage());
      return;
    }

    // Establish a connection to the database
    String url = "jdbc:mysql://localhost:3306/mydatabase";
    String username = "myusername";
    String password = "mypassword";
    Connection conn = null;
    try {
      conn = DriverManager.getConnection(url, username, password);
    } catch (SQLException e) {
      System.out.println("Error connecting to database: " + e.getMessage());
      return;
    }

    // Create a statement object
    Statement stmt = null;
    try {
      stmt = conn.createStatement();
    } catch (SQLException e) {
      System.out.println("Error creating statement: " + e.getMessage());
      return;
    }

    // Create a table
    String createTableSQL = "CREATE TABLE IF NOT EXISTS mytable (id INT PRIMARY KEY, name VARCHAR(255))";
    try {
      stmt.executeUpdate(createTableSQL);
    } catch (SQLException e) {
      System.out.println("Error creating table: " + e.getMessage());
      return;
    }

    // Insert some data
    String insertSQL = "INSERT INTO mytable (id, name) VALUES (1, 'John Doe')";
    try {
      stmt.executeUpdate(insertSQL);
    } catch (SQLException e) {
      System.out.println("Error inserting data: " + e.getMessage());
      return;
    }

    // Query the data
    String querySQL = "SELECT * FROM mytable";
    ResultSet rs = null;
    try {
      rs = stmt.executeQuery(querySQL);
    } catch (SQLException e) {
      System.out.println("Error querying data: " + e.getMessage());
      return;
    }

    // Print the results
    try {
      while (rs.next()) {
        int id = rs.getInt("id");
        String name = rs.getString("name");
        System.out.println("ID: " + id + ", Name: " + name);
      }
    } catch (SQLException e) {
      System.out.println("Error printing results: " + e.getMessage());
      return;
    }

    // Close the connection
    try {
      conn.close();
    } catch (SQLException e) {
      System.out.println("Error closing connection: " + e.getMessage());
      return;
    }
  }
}
