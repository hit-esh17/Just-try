package com.hitesh.extentReport;

import org.testng.Assert;
import org.testng.ITestResult;
import org.testng.SkipException;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.Status;
import com.aventstack.extentreports.markuputils.ExtentColor;
import com.aventstack.extentreports.markuputils.MarkupHelper;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;
import com.aventstack.extentreports.reporter.configuration.Theme;

public class BasicExtentReport {

	ExtentSparkReporter htmlReporter;
	ExtentReports reports;
	ExtentTest test;
	
	@BeforeTest
	public void startReport()
	{
		htmlReporter =  new ExtentSparkReporter("ExtentReprt.html");
		reports = new ExtentReports();
		reports.attachReporter(htmlReporter);
		
		//add environment details
		
		reports.setSystemInfo("Machine", "testpc1");
		reports.setSystemInfo("Os", "windows");
		reports.setSystemInfo("user", "Hitesh");
		reports.setSystemInfo("Browser", "Edge");
		
		// change look 
		htmlReporter.config().setDocumentTitle("Extent Report Demo");
		htmlReporter.config().setReportName("Test Report");
		htmlReporter.config().setTheme(Theme.STANDARD);
		htmlReporter.config().setTimeStampFormat("EEEE,MMMM dd , yyyy , hh:mm a '('zzz')' ");
		
	}
	@Test
	public void LaunchBrowserAndOpenURL()
	{
		test = reports.createTest("LaunchBrowser and Open URL");
		Assert.assertTrue(true);
		
	}
	@Test
	public void VerufyTitle()
	{
		test = reports.createTest("Verify Title");
		Assert.assertTrue(false);
		
	}
	@Test
	public void VerufyLogo()
	{
		test = reports.createTest("Verify Logo");
		Assert.assertTrue(true);
		
	}
	
	@Test
	public void VerufyEmail()
	{
		test = reports.createTest("Verify Email");
		throw new SkipException("skip it with exception"); 
		
	}
	
	@Test
	public void VerufyUserName()
	{
		test = reports.createTest("Verify Username");
		Assert.assertTrue(true);
		
	}
	
	@AfterMethod
	public void getTestResult(ITestResult result)
	{
		if(result.getStatus() == ITestResult.FAILURE)
		{
			test.log(Status.FAIL,MarkupHelper.createLabel(result.getName()+"FAIL",ExtentColor.RED));	
		}
		else if (result.getStatus() == ITestResult.SUCCESS)
		{
			test.log(Status.FAIL,MarkupHelper.createLabel(result.getName()+"FAIL",ExtentColor.GREEN));	
		}
		else if (result.getStatus() == ITestResult.SKIP)
		{
			test.log(Status.SKIP,MarkupHelper.createLabel(result.getName()+"FAIL",ExtentColor.YELLOW));	
		}
	}
	@AfterTest
	public void tear()
	{
		reports.flush();
	}
	
}
