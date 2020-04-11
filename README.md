package Library;

public class Test {

	public static void main(String[] args) {

		Book b1 = new Book(234, "Bubu", 34);
		System.out.println(b1);

		Book b2 = new Book(4367, "Dudu & Dan", 43);
		System.out.println(b2);

		Bestseller b3 = new Bestseller("children book", 30000, 60, "Beautiful and ugly", 3213);
		System.out.println(b3);

		Bestseller b4 = new Bestseller("Cook book", 3000, 89, "Kitchen", 678);
		System.out.println(b4);

		Book b5 = new Book(3505, "Tuti", 60);
		System.out.println(b1);

		Book b6 = new Book(656, "loli", 77);
		System.out.println(b6);

		Book[] books = { b1, b2, b3, b4, b5, b6 };

		int[] inStock = { 4, 57, 76, 23, 567, 45 };

		Storage s1 = new Storage(books, inStock);
		System.out.println(s1);
		System.out.println();

		System.out.println("********addBook*********");

		Book b7 = new Book(345, "abc", 45);
		System.out.println(b7);

		s1.addBook(b7, 100);
		System.out.print(s1.getBooks().length);
		System.out.println();

		System.out.println("******rentBook******");
		s1.rentBook(b7);

		for (int i = 0; i < s1.getInStock().length; i++) {
			System.out.print(s1.getInStock()[i] + " ");
		}
		System.out.println();

		System.out.println("********returnBook******");
		s1.returnbook(b7);
		for (int i = 0; i < s1.getInStock().length; i++) {
			System.out.print(s1.getInStock()[i] + " ");
		}
		System.out.println();
		System.out.println("********getinStock*****");
		s1.getInStock(b7);
		System.out.println(s1.getInStock(b7));
	}

}


package Library;

public class Bestseller extends Book {

	private String summery;
	private int worldCopies;

	public Bestseller(String summry, int worldCopies, double price, String name, int id) {
		super(id, name, price);
		this.summery = summery;
		this.worldCopies = worldCopies;

	}

	public String getSummery() {
		return summery;
	}

	public void setSummery(String summery) {
		this.summery = summery;
	}

	public int getWorldCopies() {
		return worldCopies;
	}

	public void setWorldCopies(int worldCopies) {
		this.worldCopies = worldCopies;
	}

	@Override
	public String toString() {
		return "Bestseller [summery=" + summery + ", worldCopies=" + worldCopies + ", toString()=" + super.toString()
				+ "]";
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((summery == null) ? 0 : summery.hashCode());
		result = prime * result + worldCopies;
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Bestseller other = (Bestseller) obj;
		if (summery == null) {
			if (other.summery != null)
				return false;
		} else if (!summery.equals(other.summery))
			return false;
		if (worldCopies != other.worldCopies)
			return false;
		return true;
	}

}
package Library;

public class Book {
	private int id;

	private String name;

	private double price;

	public Book(int id, String name, double price) {
		this.id = id;
		this.name = name;
		this.price = price;

	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return "Book [ name=" + name + ", price=" + price + "]";
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + id;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		long temp;
		temp = Double.doubleToLongBits(price);
		result = prime * result + (int) (temp ^ (temp >>> 32));
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Book other = (Book) obj;
		if (id != other.id)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		if (Double.doubleToLongBits(price) != Double.doubleToLongBits(other.price))
			return false;
		return true;
	}

}


package Library;

import java.util.Arrays;

public class Storage {

	private Book[] books;

	private int[] inStock;

	public Storage(Book[] books, int[] inStock) {
		this.books = books;
		this.inStock = inStock;
	}

	public Book[] getBooks() {
		return books;
	}

	public void setBooks(Book[] books) {
		this.books = books;
	}

	public int[] getInStock() {
		return inStock;
	}

	public void setInStock(int[] inStock) {
		this.inStock = inStock;
	}

	@Override
	public String toString() {
		return "Storage [books=" + Arrays.toString(books) + ", inStock=" + Arrays.toString(inStock) + ", getBooks()="
				+ Arrays.toString(getBooks()) + ", getInStock()=" + Arrays.toString(getInStock()) + ", toString()="
				+ super.toString() + "]";
	}

	public void addBook(Book book, int amount) {

		for (int i = 0; i < books.length; i++) {

			if (books[i] != null && books[i].equals(book)) { // בודקים אם הספר שרוצים להכניס כבר קיים בסטוק
				// ובודקים אם הספר שונה מאפס ,זאת אומרת לא ניתן להשוות משהו שהוא אפס
				inStock[i] = inStock[i] + amount;// אם קיים מעתכנים את הכמות שלו
				return;

			} else if (books[i] == null) {// יש מקום להכניס ספר חדש
				books[i] = book;
				inStock[i] = amount;
				return;
			}

		}
		// הקצאת מערך זמני כדי להכניס ספר שביעי
		// אם עברתי על המערך ולא מצאתי שיש מקום , עושים מערכים זמניים
		int len = books.length;
		Book[] tmpBooks = new Book[len];// הגדרת שני מערכי עזר
		int[] tmpinStock = new int[len];
		for (int i = 0; i < books.length; i++) {// העתקת שני מערכי עזר
			tmpBooks[i] = books[i];
			tmpinStock[i] = inStock[i];
		}

		books = new Book[len + 1];// הרחבה של הארוך המערך המקוריתהקצאת מקום נוסף למערך הקיים
		inStock = new int[len + 1];

		for (int i = 0; i < len; i++) {// מעתיקים בחזרה למערך המקורי עם האורך המקורי,השישה הראשוני
			books[i] = tmpBooks[i];
			inStock[i] = tmpinStock[i];
		}

		books[len] = book;// בכתובת האחרונה שמים ספר חדש ומעדכנים את גם את המקום באחסון
		inStock[len] = amount;

	}

	public void rentBook(Book book) {
		for (int i = 0; i < books.length; i++) {
			if (books[i].equals(book)) {// בודקים אם יש ספר זהה להשכרה
				if (inStock[i] > 0) {// כדי שלא נוריד והיהי שלילי
					inStock[i] = inStock[i] - 1;// אם יש מעדכנים את הכמות,מורידים אחד
					System.out.println("you could rent a book");
					return;// להחזיר,אין טעם להמשיך כי הבן אדם שכר את הספר
				} else {
					System.out.println("The book is not available");// אם קיים אבל כרגע לא במדף

				}

			}
		}
		System.out.println("We dont have a book");// אם אין בכלל את הספר
	}

	public void returnbook(Book book) {// המתודה מחזירה ספר קיים
		for (int i = 0; i < books.length; i++) {
			if (books[i] != null && books[i].equals(book)) {// בודקת אם יהספר שונה מאפס רק אז ניתן להפעיל את המתודה
															// שבודקת אם הספר הזהה קיים
				inStock[i] = inStock[i] + 1;// מחזירה את הספר
				return;
			}

		}
		System.out.println("Sorry are you sure this book is belong to us?");// בדקנו והבנו שאין ספר כזה במערכת בכלל

	}

	public int getInStock(Book book) {
		for (int i = 0; i < books.length; i++) {
			if (books[i] != null && books[i].equals(book)) {
				return inStock[i];
			}
		}

		return 0;
	}
}

