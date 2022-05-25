package finalProject;

import java.io.File;
import java.io.IOException;
import java.util.InputMismatchException;
import java.util.Scanner;

public class FinalProject {
	private Item[] items = new Item[100];
	private Scanner input = new Scanner(System.in);

	
	public static void main(String[] args ) throws IOException {
		
		
		FinalProject run = new FinalProject();
		run.mainMenu();
		
	}//End main
	
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	public void mainMenu() throws InputMismatchException, IOException{
		
		//Populates catalog
		File file = new File("./catalog.txt");
		Scanner sc = new Scanner(file);
		//sc.useDelimiter("\\  ");
		//id, name, price, quantity, string temp
		for (int i = 0; i < items.length; i++) {
		while (sc.hasNext()) {
			
			int id = sc.nextInt();
			String name = sc.next();
			Double price = sc.nextDouble();
			int quantity = sc.nextInt();
			items[i] = new Item(id, name, price, quantity);


			break;
			}
		}
			
		
		sc.close();
		
	
		/*
		 Admin login
		 User: admin
		 Pass: password
		 */
		
		String username = "admin";
		String password = "password";
		boolean exit = false;
		
		do {
		
		System.out.println("1 - Admin Menu");
		System.out.println("2 - User Menu");
		System.out.println("3 - Exit");

		int option = input.nextInt();
		while (option < 1 || option > 3)
		{
			System.out.println("Error.  Please enter valid choice: ");
			option = input.nextInt();
		}
		
		
		switch (option) {
		case 1:
			// verify the admin login

			String tempUser = "default";
			String tempPass = "default";
			while (tempUser != username && tempPass != password) {
				System.out.println("Username: ");
				tempUser = input.next();
				System.out.println("Password: ");
				tempPass = input.next();
				
				if (tempUser.equals(username) && tempPass.equals(password)) {
					adminMenu();
					break;
				}
				else
					System.out.println("Error.  Invalid username or password.\n");
				
			}
			break;
			
		
		case 2: 
			userMenu();
			break;

		case 3:
			System.out.println("Are you sure you would like to exit?  Type y or n: ");
			char confirm = input.next().toLowerCase().charAt(0);
			if (confirm == 'y')
				exit = true;
			else 
				exit = false;
			break;		}
		
		}while (!exit);
	}//End mainMenu

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	public void adminMenu() throws IOException {
		System.out.println("\n1 - Add new item");
		System.out.println("2 - Search and update item");
		System.out.println("3 - Search and delete item");		
		int option = input.nextInt();
		int found = -1;
		switch (option) {
		case 1:  //Add item
			addItem();
			break;

		case 2:  //Update Item
			System.out.println("Enter an item name to update: \n");

				found = searchForItem();

				if (found != -1) {
					updateItem(found);
				}

				break;
			

		case 3:  //Delete Item
			System.out.println("Enter an item name to delete: \n");
			found = searchForItem();
			if (found != -1) {
				deleteItem(found);
			}
			break;

		case 4: //Main menu
			return;
		}
	}//End adminMenu

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


	public void userMenu() throws IOException {
		System.out.println("\n1 - Search for Item");
		System.out.println("2 - Purchase Item");
		int option = input.nextInt();
		
		while (option < 1 || option > 2)
		{
			System.out.println("Error.  Please enter valid choice: ");
			option = input.nextInt();
		}
		
		int found = -1;
		switch (option) {
		case 1:  //Display Items
			
			displayAllItems();
			break;

		case 2:  //Purchase Items
			System.out.println("What item would you like to purchase?\n");
			found = searchForItem();
			if (found != -1) {
				purchaseItem(found);			}
			break;

		default: //Main menu
			return;
		}
	}//End userMenu

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


	private void displayAllItems() throws IOException{

		System.out.println("|\tID\t|\tName\t|\tPrice\t|\tQuantity|");
		for (int i = 0; i < items.length; i++) {
			if (items[i] != null){
				System.out.println("|\t"+items[i].getID()+"\t|\t"+items[i].getName()+"\t|\t"+items[i].getPrice()+"\t|\t"+items[i].getQuantity()+"\t|\t");
			}
		}
	}//End displayItems

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	public int searchForItem(){
		input.nextLine();
		// get a string to search from the user
		String searchText = input.nextLine().toLowerCase();
		// loop through the array looking for books which contain the search text
		boolean[] matches = new boolean[100];
		boolean found = false;
		for (int i = 0; i < items.length; i++) {

		if (items[i] != null) {
		// if this book has a match
		if (items[i].getName().toLowerCase().contains(searchText)) {
		matches[i] = true;
		found = true;
		}
		}
		}

		if (!found) {
		System.out.println("Item not found.");
		return -1;
		}
		// Displays the titles of all the items that matched.
		for (int i = 0; i < items.length; i++) {
		if (matches[i]) {
		System.out.println(i + ". " + items[i].getName());
		}
		} 
		
		do {
		try {
		// User chooses one of the titles.
		System.out.println("\nEnter the number next to the item you're looking for: ");
		int selectedItem = input.nextInt();
		System.out.println("ID: " +items[selectedItem].getID()+"  Name: "+items[selectedItem].getName()+"  Price: "+items[selectedItem].getPrice()+"  Quantity: "+items[selectedItem].getQuantity()+"\n");		
		return selectedItem;
		} catch (InputMismatchException e) {
		System.out.println("Enter a number next time.");
		input.next();
		}
		} while (true);
		}
	

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	private void deleteItem(int index) {
		boolean found = false;
		
		// loop through array
		for (int i = 0; i < items.length; i++)
		{
			// if this is a valid object and the correct object
			if (items[i] != null && items[i].getID()-1 == index)
			{
				System.out.println("Item: "+items[index].getName()+", has been deleted.\n" );
				// delete object
				items[i] = null;

				found = true;

				break;
			}
		}
		
		
	}//End deleteItems

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	private void updateItem(int index) {
		boolean found = false;
		Scanner keyboard = new Scanner(System.in);
		System.out.println("Enter a new item price: ");
		Double price = keyboard.nextDouble();
		System.out.println("Enter a new item quantity: ");
		int quantity = keyboard.nextInt();
		found = false;
		
		for (int i=0;i<items.length;i++) {
			if (items[i] != null && items[i].getID()-1 == index) {
				items[i].setPrice(price);
				items[i].setQuantity(quantity);
				
				found = true;
				break;
			}
		}
		
		if (!found) {
			System.out.println("Error, item not found.");
		}
		
		
	}//End updateItem

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	//Fix a bit more, works right now.  Fix for loop, only allows 1 addition
	
	private void addItem() throws IOException{
		int nextIDNumber = 3;
		Scanner keyboard = new Scanner(System.in);
		System.out.println("Enter item name: ");
		String name = keyboard.next();
		System.out.println("Enter item price: ");
		Double price = keyboard.nextDouble();
		System.out.println("Enter item quantity: ");
		int quantity = keyboard.nextInt();
	
		for (int i = nextIDNumber; i < items.length; i++)
			{
				//Check if empty
				if (items[nextIDNumber] == null)
				{
					items[i] = new Item(++nextIDNumber, name, price, quantity);
				}
				break;
			}

		
	}//End addItem

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

	
	private void purchaseItem(int index) {

		Scanner keyboard = new Scanner(System.in);
		System.out.println("Enter quantity you would like to purchase: ");
		int option = input.nextInt();
		boolean found = false;
		
		while (option > items[index].getQuantity())
		{
			System.out.println("Error.  Invalid quantity.  Input a valid amount: ");
			option = input.nextInt();
		}
		
		for (int i=0;i<items.length;i++) {
			if (items[i] != null && items[i].getID()-1 == index) {
				
				//Calculates cost of item purchased w/ quantity and tax
				double tax = (items[i].getPrice()*option)*.07;
				double total = (items[i].getPrice()*option)+tax;
				System.out.println("\nItem: "+items[i].getName()+"\nQuantity: "+option+"\nTotal Price: "+total+"\n");
				
				//Updates amount in catalog
				int newQuantity = items[index].getQuantity()-option;
				items[i].setQuantity(newQuantity);
				
				found = true;
				break;
			}
		}
		
		if (!found) {
			System.out.println("Error, item not found.");
		}
		
		
	}//End purchaseItem
	
	
}//End FinalProject class


/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
class Item{
	private int id;
	private String name;
	private double price;
	private int quantity;
	
	
	public Item(int id, String name, double price, int quantity) {
		setID(id);
		setName(name);
		setPrice(price);
		setQuantity(quantity);
	}
	
	public void setID(int id) {
		if (id > 0)
			this.id = id;
	}
	
	public int getID() {
		return id;
	}
	
	public void setName(String name) {
		this.name = name;
	}
	
	public String getName() {
		return name;
	}
	
	public void setPrice(double price) {
		if(price >=0)
			this.price = price;
	}
	
	public double getPrice() {
		return price;
	}
	
	public void setQuantity(int quantity) {
		if (quantity >= 0)
			this.quantity = quantity;
	}
	
	public int getQuantity() {
		return quantity;
	}
	
	
}//End Item class
