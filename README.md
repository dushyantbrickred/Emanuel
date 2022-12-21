import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;

import io.github.bonigarcia.wdm.WebDriverManager;

public class SaucedemoAssessment {

	public static void main(String[] args) throws InterruptedException {

		//Launch a browser
		WebDriver driver = WebDriverManager.edgedriver().create();
		driver.manage().window().maximize();
		driver.manage().deleteAllCookies();
		driver.get("https://www.saucedemo.com/");
		Thread.sleep(1000);
		

		driver.findElement(By.id("user-name")).sendKeys("standard_user");
		Thread.sleep(1000);
		driver.findElement(By.id("password")).sendKeys("secret_sauce");
		Thread.sleep(1000);
		driver.findElement(By.id("login-button")).click();
		Thread.sleep(1000);
		
		
		driver.findElement(By.xpath("//select[@class='product_sort_container']")).click();	
//		Actions act = new Actions(driver);
//		act.clickAndHold(SortingDropdown).perform();
		Thread.sleep(2000);
		driver.findElement(By.xpath("(//*[text()='Price (low to high)'])")).click();
		Thread.sleep(2000);
		driver.findElement(By.xpath("(//*[text()='Add to cart'])[1]")).click();
		Thread.sleep(1000);
		
		String item1= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[1]")).getText();
		item1 = item1.replaceFirst("[$]", "");
		float Price1 = Float.valueOf(item1);
		
		String item2= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[2]")).getText();
		item2 = item2.replaceFirst("[$]", "");
		float Price2 = Float.valueOf(item2);
		
		String item3= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[3]")).getText();
		item3 = item3.replaceFirst("[$]", "");
		float Price3 = Float.valueOf(item3);
		
		String item4= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[4]")).getText();
		item4 = item4.replaceFirst("[$]", "");
		float Price4 = Float.valueOf(item4);
		
		String item5= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[5]")).getText();
		item5 = item5.replaceFirst("[$]", "");
		float Price5 = Float.valueOf(item5);
		
		String item6= driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[6]")).getText();
		item6 = item6.replaceFirst("[$]", "");
		float Price6 = Float.valueOf(item6);
		
		Thread.sleep(1000);
		
		
		//Adding item with higher price
		if(Price1<=Price2 & Price2<=Price3 & Price3<=Price4 & Price4<=Price5 & Price5<=Price6 )
			
		{	
			
			JavascriptExecutor	jv	=	(JavascriptExecutor)driver;
			WebElement sorting = driver.findElement(By.xpath("(//*[text()='Add to cart'])[5]"));
			jv.executeScript("arguments[0].scrollIntoView()",sorting);
			Thread.sleep(1000);
			driver.findElement(By.xpath("(//*[text()='Add to cart'])[5]")).click();	
				
		}
		else	throw new AssertionError("Sorting id broken");
		
		Thread.sleep(1000);
		driver.findElement(By.xpath("//*[@class='shopping_cart_link']")).click();	
		Thread.sleep(1000);

		
		//Validate that the items are added into the cart
		
		Boolean Addeditem1 = driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[1]")).isDisplayed();
		Boolean Addeditem2 = driver.findElement(By.xpath("(//div[@class=\"inventory_item_price\"])[2]")).isDisplayed();
		
		if(Addeditem1 & Addeditem2) {
			driver.quit();
		}
		else	throw new AssertionError("Items are not added");
		
			
		

	}

}
