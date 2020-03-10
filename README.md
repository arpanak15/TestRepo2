package test;

import org.junit.After;
import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;
import java.util.Random;
import java.util.concurrent.TimeUnit;

    public class junit {
    WebDriver driver;
    Random random = new Random();
    @Before
    public void setUp() {
        System.setProperty("webdriver.chrome.driver", "C:\\Users\\Test\\Downloads\\chromedriver_win32\\chromedriver.exe");
        driver = new ChromeDriver();
        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
        String url = "http://automationpractice.com/";
        driver.get(url);
    }
    @Test
    public void checkRegistration(){
        String random_email = "mojemail"+random.nextInt(999999)+"@wp.pl";
        String random_password = "1qaz"+random.nextInt(999999);
        driver.findElement(By.cssSelector(".login")).click();
        driver.findElement(By.xpath("//input[@name='email_create']")).sendKeys(random_email);
        driver.findElement(By.xpath("//input[@name='email_create']")).sendKeys(Keys.ENTER);
        driver.findElement(By.id("customer_firstname")).sendKeys("Jan");
        driver.findElement(By.id("customer_lastname")).sendKeys("Nowak");
        driver.findElement(By.id("passwd")).sendKeys(random_password);
        driver.findElement(By.id("address1")).sendKeys("Grochowska 2");
        driver.findElement(By.id("city")).sendKeys("Warszawa");
        driver.findElement(By.id("postcode")).sendKeys("57212");
        Select dropdown;
        dropdown = new Select(driver.findElement(By.xpath("//*[@name='days']")));
        dropdown.selectByValue("12");
        dropdown = new Select(driver.findElement(By.xpath("//*[@name='months']")));
        dropdown.selectByValue("4");
        dropdown = new Select(driver.findElement(By.xpath("//*[@name='years']")));
        dropdown.selectByValue("1987");
        dropdown = new Select(driver.findElement(By.id("id_state")));
        dropdown.selectByValue("4");
        driver.findElement(By.id("newsletter")).click();
        driver.findElement(By.id("phone_mobile")).sendKeys("3562178561");
        driver.findElement(By.id("submitAccount")).click();
        Assert.assertTrue(driver.findElement(By.cssSelector(".logout")).isDisplayed());
        String name_on_page = driver.findElement(By.cssSelector(".header_user_info span")).getText();
        Assert.assertEquals("Jan Nowak", name_on_page);
    }
    @After
    public void tearDown() throws InterruptedException {
        driver.close();
    }
}
