
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using OpenQA.Selenium.Chrome;
using OpenQA.Selenium;
using OpenQA.Selenium.Support.UI;
using SeleniumExtras.WaitHelpers;
using System.Collections.Generic;
using Helpers;


namespace TestScript

{


    [TestClass]
    public class UnitTest1
    {
        public void SetElementValue(string value, By objectPath)
        {
            var element = _driver.FindElement(objectPath);
            element.SendKeys(value);
        }
        public void WaitVisible(By element)
        {
            var wait = new WebDriverWait(_driver, new TimeSpan(0, 0, 15));
            wait.Until(ExpectedConditions.ElementIsVisible(element));
        }
        public void ClickElement(By objectPath)
        {
            var element = _driver.FindElement(objectPath);
            element.Click();
        }
        public void AssertElementText(string text, By objectPath)
        {
            var element = _driver.FindElement(objectPath);
            Assert.IsTrue(element.Text == (text));
        }

        [TestInitialize]

        public void InitializeTest()
        {
            _driver = new ChromeDriver();
        }


        [TestCleanup]
        public void TearDown()
        {
            _driver.Quit();
        }




        [TestMethod]
        public void Login_Success_ShowAccountDashBoard()
        {
            var wait = new WebDriverWait(_driver, new TimeSpan(0, 0, 15));
            //Arrange
            _driver.Navigate().GoToUrl(_url);
            WaitVisible(TextUserEmail);
            WaitVisible(TextUserPassword);


            //Act
            SetElementValue("", TextUserEmail);
            SetElementValue("", TextUserPassword);
            ClickElement(SignInButton);



            //Assert
            wait.Until(ExpectedConditions.UrlContains("admin/accounts"));
            Assert.IsTrue(_driver.Url.Contains("admin/accounts"));

        }

        [TestMethod]
        public void Login_InvalidPassword_ShowErrorMessage()
        {
            //Arrange
            _driver.Navigate().GoToUrl(_url);
            WaitVisible(TextUserEmail);
            WaitVisible(TextUserPassword);
            //Act
            SetElementValue("", TextUserEmail);
            SetElementValue("", TextUserPassword);
            ClickElement(SignInButton);
            //Assert
            WaitVisible(errorMessagePath);
            var errorMessage = _driver.FindElement(errorMessagePath);
            Assert.IsTrue(errorMessage.Text == ("Invalid email address or password"), "actual Message is not match expetected Result");
        }

        [TestMethod]
        public void Login_AccountUser_ShowError()
        {
            //Arrange
            _driver.Navigate().GoToUrl(_url);
            WaitVisible(TextUserEmail);
            WaitVisible(TextUserPassword);
           
            //Act
            SetElementValue("", TextUserEmail);
            SetElementValue("", TextUserPassword);
            ClickElement(SignInButton);
            //Assert
            WaitVisible(errorMessagePath);
            var errorMessage = _driver.FindElement(errorMessagePath);
            Assert.IsTrue(errorMessage.Text == ("Invalid email address or password"), "actual Message is not match expetected Result");
        }

        [TestMethod]
        public void ForgotPassword_SubmitBlankEmail_ErrorMessage()
        {
            _driver.Navigate().GoToUrl(_url);
            WaitVisible(TextUserEmail);
            WaitVisible(TextUserPassword);
            ClickElement(ForgotPassword);
            //Act
            ClickElement(ForgotPasswordButton);
            //Assert
            WaitVisible(ForgotPasswordError);
            AssertElementText("Please enter your email address", ForgotPasswordError);
        }

        [TestMethod]
        public void ForgotPassword_SendForgotPasswordEmail_Successful()
        {
            //Arrange

            _driver.Navigate().GoToUrl(_url);
            WaitVisible(TextUserEmail);
            WaitVisible(TextUserPassword);
            ClickElement(ForgotPassword);
            //Act
            SetElementValue("", TextUserEmail);
            ClickElement(ForgotPasswordButton);
            //Assert
            WaitVisible(ForgotPasswordNotification);
            AssertElementText("You will receive an email shortly to reset your password", ForgotPasswordNotification);
        }


        //Setup Test Data
        IWebDriver _driver;
        string _url = "";

        //Sign In Page
        public By TextUserEmail = By.Id("email");
        public static By TextUserPassword = By.XPath("//*[@id=\"signinForm\"]/div[2]/input");
        public static By SignInButton = By.XPath("//*[@id=\"signinForm\"]/div[4]/input");
        public static By errorMessagePath = By.XPath("//*[@id=\"signinForm\"]/div[2]/div[2]/div");
        public By ForgotPassword = By.XPath("//*[@id=\"signinForm\"]/div[3]/a");

        //Forgot Password Page
        public By ForgotPasswordButton = By.XPath("//*[@id=\"wrapper\"]/div/section/div/div[1]/div/div/div/form/div[2]/input");
        public By ForgotPasswordError = By.XPath("//*[@id=\"wrapper\"]/div/section/div/div[1]/div/div/div/form/div[1]/div[1]");
        public By ForgotPasswordNotification = By.XPath("//*[@id=\"wrapper\"]/div/section/div/div[2]/div");
   }
}
