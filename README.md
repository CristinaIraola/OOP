# OOP

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.*;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.Locale;
import java.util.concurrent.TimeUnit;
import javax.swing.*;

	public class user_menu {

		public static void main(String UID) {
			String[] name = {"Tin's Book Rental "};
			String[] book = {"Scorching Love","He's Into Her","Tears Of Love"};
			String[] author = {" By Jonaxx","By Maxinejiji","By MsKindGirl"};
			double year = 2020;
			int[] copy = {2,3,4};
			
			System.out.println("TIN'S BOOK RENTAL  ");
			System.out.println("***********************");
	
			JFrame f=new JFrame("User Functions"); 
			JButton view_but=new JButton("View Books"); {
			view_butsetBounds(20,20,120,25);
			view_but.addActionListener(new ActionListener() { 
				
	    public void actionPerformed(ActionEvent e){
	       JFrame f = new JFrame("Books Available"); 
	       Connection connection = connect();
	            String sql="select * from BOOKS"; 
	            try {
	                Statement stmt = connection.createStatement(); 
	                 stmt.executeUpdate("USE LIBRARY"); 
	                stmt=connection.createStatement();
	                ResultSet rs=stmt.executeQuery(sql);
	                JTable book_list= new JTable();
	                book_list.setModel(DbUtils.resultSetToTableModel(rs)); 
	                  
	                JScrollPane scrollPane = new JScrollPane(book_list); 
	 
	                f.add(scrollPane); 
	                f.setSize(800, 400); 
	                f.setVisible(true);
	                f.setLocationRelativeTo(null);
	            }	 catch (SQLException e1) {
	                 JOptionPane.showMessageDialog(null, e1);
	            }               
	             
	    }
	    }
	    );
	     
			JButton my_book=new JButton("My Books");
			my_book.setBounds(150,20,120,25);
			my_book.addActionListener(new ActionListener() { 
	        public void actionPerformed(ActionEvent e){
	             
	               
	            JFrame f = new JFrame("My Books");
	            Connection connection = connect();
	            String sql="select distinct issued.*,books.bname,books.genre,books.price from issued,books " + "where ((issued.uid=" + UID_int + ") and (books.bid in (select bid from issued where issued.uid="+UID_int+"))) group by iid";
	            String sql1 = "select bid from issued where uid="+UID_int;
	            try {
	                Statement stmt = connection.createStatement();
	                 stmt.executeUpdate("USE LIBRARY");
	                stmt=connection.createStatement();
	                ArrayList books_list = new ArrayList();
	  
	                
	                 
	                ResultSet rs=stmt.executeQuery(sql);
	                JTable book_list= new JTable(); 
	                book_list.setModel(DbUtils.resultSetToTableModel(rs)); 
	                JScrollPane scrollPane = new JScrollPane(book_list);
	 
	                f.add(scrollPane); 
	                f.setSize(800, 400);
	                f.setVisible(true);
	                f.setLocationRelativeTo(null);
	            } catch (SQLException e1) {
	                 JOptionPane.showMessageDialog(null, e1);
	            }               
	                 
	    }
	    }
	    );
	     
	     
	     
	    f.add(my_book); //add my books
	    f.add(view_but); // add view books
	    f.setSize(300,100);//400 width and 500 height  
	    f.setLayout(null);//using no layout managers  
	    f.setVisible(true);//making the frame visible 
	    f.setLocationRelativeTo(null);
	    }
	}

}
