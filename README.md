package jdbc3;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class sql2 {

	static final String url = "jdbc:mysql://localhost/college";
	static final String name = "root";
	static final String pass = "sourness";
	
	public static void main(String[] args) throws SQLException, NumberFormatException, IOException {
		Connection c = null;
		Statement s = null;
		ResultSet r = null;
		
		int choice;
		c = DriverManager.getConnection(url,name,pass);
		
		System.out.println("\n");
		System.out.println("Menu : ");
		System.out.println("1. Insert Record into table :");
		System.out.println("2. Update the exist:");
		System.out.println("3. Display all :");
		System.out.println("4. Delete the record:");
		System.out.println("5. Exit");
		
		System.out.println("Enter choice : ");
		
		BufferedReader b = new BufferedReader(new InputStreamReader(System.in));
		
		choice = Integer.parseInt(b.readLine());
		
		switch (choice) {
		case 1: {
			System.out.println("Enter first name : ");
			String firstname = b.readLine();
			
			System.out.println("Enter second name : ");
			String secondname = b.readLine();
			
			System.out.println("Enter roll no. : ");
			int roll = Integer.parseInt(b.readLine());
			
			String sql = "insert into student values(?,?,?)";
			PreparedStatement p = c.prepareCall(sql);
			
			p.setString(1 , firstname);
			p.setString(2, secondname);
			p.setInt(3, roll);
			
			p.executeUpdate();
			System.out.println("Table created....");
			break;
		}
		default:
			throw new IllegalArgumentException("Unexpected value: ");
		}
		
	}

}
