# Zervvo_Technology
package Zervvo.Project.pages;

import org.junit.jupiter.api.*;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.*;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.time.Duration;
import java.util.List;

@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class OrangeHRMAutomation {
	 WebDriver driver;

	    public static void main(String[] args) {
	        OrangeHRMAutomation test = new OrangeHRMAutomation();
	        test.setUp();
	        test.login();
	        test.pimModule();
	        test.leaveModule();
	        test.logout();
	        test.tearDown();
	    }

	    public void setUp() {
	        driver = new ChromeDriver();
	        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
	        driver.manage().window().maximize();
	    }

	    public void login() {
	        driver.get("https://opensource-demo.orangehrmlive.com/web/index.php/auth/login");
	        sleep(2000);
	        driver.findElement(By.name("username")).sendKeys("Admin");
	        driver.findElement(By.name("password")).sendKeys("admin123");
	        driver.findElement(By.xpath("//button[@type='submit']")).click();
	        sleep(3000);
	    }

	    public void pimModule() {
	        click(By.xpath("//span[text()='PIM']"));

	        // Add Employee
	        click(By.xpath("//a[text()='Add Employee']"));
	        sleep(1000);
	        driver.findElement(By.name("firstName")).sendKeys("Test");
	        driver.findElement(By.name("middleName")).sendKeys("User");
	        driver.findElement(By.name("lastName")).sendKeys("Ziegan");
	        click(By.xpath("//button[@type='submit']"));
	        sleep(2000);

	        // Search Employee
	        click(By.xpath("//a[text()='Employee List']"));
	        driver.findElement(By.xpath("//input[@placeholder='Type for hints...']")).sendKeys("Test");
	        click(By.xpath("//button[@type='submit']"));
	        sleep(2000);

	        // Edit Employee
	        click(By.xpath("//i[@class='oxd-icon bi-pencil-fill']"));
	        sleep(1000);
	        WebElement middleName = driver.findElement(By.name("firstName"));
	        middleName.clear();
	        middleName.sendKeys("Edited");
	        click(By.xpath("//button[@type='submit']"));
	        sleep(2000);

	        // Delete Employee
	        click(By.xpath("//a[text()='Employee List']"));
	        click(By.xpath("//i[@class='oxd-icon bi-trash']"));
	        click(By.xpath("//button[text()=' Yes, Delete ']"));
	        sleep(2000);

	        // Data Import
	        click(By.xpath("//span[text()='Configuration ']"));
	        click(By.xpath("//a[text()='Data Import']"));
	        sleep(2000);
	    }

	    public void leaveModule() {
	        click(By.xpath("//span[text()='Leave']"));

	        // Apply Leave
	        click(By.xpath("//a[text()='Apply']"));
	        sleep(2000);

	        // Leave List
	        click(By.xpath("//a[text()='Leave List']"));
	        sleep(2000);

	        // My Leave
	        click(By.xpath("//a[text()='My Leave']"));
	        sleep(2000);

	        // Assign Leave
	        click(By.xpath("//a[text()='Assign Leave']"));
	        sleep(2000);

	        // Manage Entitlements
	        click(By.xpath("//span[text()='Entitlements ']"));
	        click(By.xpath("//a[text()='Add Entitlements']"));
	        sleep(2000);
	    }
	    
	    public void waitAndClick(By locator) {
	        new WebDriverWait(driver, Duration.ofSeconds(10))
	            .until(ExpectedConditions.elementToBeClickable(locator))
	            .click();
	    }

	    public void logout() {
	        click(By.xpath("//span[@class='oxd-userdropdown-tab']"));
	        click(By.xpath("//a[text()='Logout']"));
	        sleep(2000);
	    }

	    public void tearDown() {
	        driver.quit();
	    }

	    private void click(By locator) {
	        driver.findElement(locator).click();
	    }

	    private void sleep(long millis) {
	        try {
	            Thread.sleep(millis);
	        } catch (InterruptedException ignored) {}
	    }
	}
