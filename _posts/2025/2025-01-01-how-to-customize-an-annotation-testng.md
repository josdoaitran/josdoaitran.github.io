---
layout: post
title:  "How to customize a annotation on TestNG"
author: donald
categories: [ coding, testng, tutorial ]
image: assets/images/general-sharing/testng-logo.png
---

Creating and using custom annotations in TestNG involves several steps. You need to define your custom annotation, create an annotation processor, and then use the annotation in your tests. Below is an example of how to do this:

*Define the Custom Annotation*

Create a custom annotation @CustomTest.
1. **Create an Annotation Processor**: Implement the logic that should be executed when the annotation is present.
2. **Use the Custom Annotation in Tests**: Apply the annotation to your test methods and process it.

Here’s a detailed step-by-step example:
**Step 1: Define the Custom Annotation**

Create a custom annotation called @CustomTest.

```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface CustomTest {
    String value() default "Default Value";
}
```

**Step 2: Create an Annotation Processor**

Create a listener that processes the annotation. This listener will implement the ITestListener interface.

```java
import org.testng.ITestContext;
import org.testng.ITestListener;
import org.testng.ITestResult;
import java.lang.reflect.Method;

public class CustomAnnotationProcessor implements ITestListener {
    
    @Override
    public void onTestStart(ITestResult result) {
        Method method = result.getMethod().getConstructorOrMethod().getMethod();
        if (method.isAnnotationPresent(CustomTest.class)) {
            CustomTest customTest = method.getAnnotation(CustomTest.class);
            System.out.println("Custom annotation value: " + customTest.value());
        }
    }

    @Override
    public void onTestSuccess(ITestResult result) {
        // Implement other methods if needed
    }

    @Override
    public void onTestFailure(ITestResult result) {
        // Implement other methods if needed
    }

    @Override
    public void onTestSkipped(ITestResult result) {
        // Implement other methods if needed
    }

    @Override
    public void onTestFailedButWithinSuccessPercentage(ITestResult result) {
        // Implement other methods if needed
    }

    @Override
    public void onStart(ITestContext context) {
        // Implement other methods if needed
    }

    @Override
    public void onFinish(ITestContext context) {
        // Implement other methods if needed
    }
}
```

**Step 3: Use the Custom Annotation in Tests**

Apply the @CustomTest annotation to your test methods and configure TestNG to use your listener.

```java
import org.testng.annotations.Listeners;
import org.testng.annotations.Test;

@Listeners(CustomAnnotationProcessor.class)
public class MyTests {

    @Test
    @CustomTest(value = "Custom Annotation Value for Test 1")
    public void testMethod1() {
        System.out.println("Executing testMethod1");
    }

    @Test
    @CustomTest(value = "Custom Annotation Value for Test 2")
    public void testMethod2() {
        System.out.println("Executing testMethod2");
    }

    @Test
    public void testMethod3() {
        System.out.println("Executing testMethod3");
    }
}
```

**Explanation:**

1.**Define the Custom Annotation**:

•	The @Retention(RetentionPolicy.RUNTIME) ensures that the annotation is available at runtime.
•	The @Target(ElementType.METHOD) specifies that this annotation can only be applied to methods.

2.**Create an Annotation Processor**:

•	The CustomAnnotationProcessor implements ITestListener to hook into the test lifecycle.
•	The onTestStart method is overridden to check if the method has the @CustomTest annotation and print its value.

3.**Use the Custom Annotation in Tests**:

•	The @Listeners(CustomAnnotationProcessor.class) annotation tells TestNG to use the custom listener for the test class.
•	The @CustomTest annotation is applied to test methods with specific values.

**Running the Tests**
When you run your TestNG tests, the output will show the custom annotation values:

```java
Custom annotation value: Custom Annotation Value for Test 1
Executing testMethod1
Custom annotation value: Custom Annotation Value for Test 2
Executing testMethod2
Executing testMethod3
```

This approach allows you to create and use custom annotations in your testing framework rpoject with TestNG, enabling you to add custom behavior to your tests.
