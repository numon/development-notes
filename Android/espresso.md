# Espresso

There are 6 types of annotations that can be applied to the methods used inside the test class,which are @Test, @Before, @BeforeClass, @After, @AfterClass, @Rule
![Hooks](images/hook.jpeg)

Important things to note is that:

The activity will be launched using the @Rule before test code begins
By default the rule will be initialised and the activity will be launched(onCreate, onStart, onResume) before running every @Before method
Activity will be Destroyed(onPause, onStop, onDestroy) after running the @After method which in turn is called after every @Test Method
The activity’s launch can be postponed by setting the launchActivity to false in the constructor of ActivityTestRule ,in that case you will have to manually launch the activity before the tests

## API components
The main components of Espresso include the following:

*Espresso* – Entry point to interactions with views (via onView() and onData()). Also exposes APIs that are not necessarily tied to any view, such as pressBack().
*ViewMatchers* – A collection of objects that implement the Matcher<? super View> interface. You can pass one or more of these to the onView() method to locate a view within the current view hierarchy.
*ViewActions* – A collection of ViewAction objects that can be passed to the ViewInteraction.perform() method, such as click().
*ViewAssertions* – A collection of ViewAssertion objects that can be passed the ViewInteraction.check() method. Most of the time, you will use the matches assertion, which uses a View matcher to assert the state of the currently selected view.

## Machers

![Hooks](images/matchers.png)
Espresso uses onView (Matcher<View> viewMatcher) method to find a particular view among the View hierarchy. onView() method takes a Matcher as argument. Espresso provides a number of these ViewMatchers which can be found in this Espresso Cheat sheet.

Every UI element contains properties or attributes which can be used to find the element.Suppose for finding an element with

`android:id=“+id/login_button”`
We can write

`Espresso.onView(withId(R.id.login_button))`

## Performing actions on the View
![actions](images/actions.png)

`Espresso.onView(withId(R.id.login_button)).perform(click())`

## Checking the ViewAssertions
![actions](images/Assertion.png)
`Espresso.onView(withId(R.id.login_result)).check(matches(withText(R.string.login_success)))`

## Example 
```java
package com.package.model.page;

import com.package.model.R;
import com.package.model.view.activity.EnrollmentActivity;

import org.junit.Rule;
import org.junit.Test;
import org.junit.runner.RunWith;

import androidx.test.filters.LargeTest;
import androidx.test.rule.ActivityTestRule;
import androidx.test.runner.AndroidJUnit4;

import static androidx.test.espresso.Espresso.onView;
import static androidx.test.espresso.action.ViewActions.click;
import static androidx.test.espresso.action.ViewActions.typeText;
import static androidx.test.espresso.assertion.ViewAssertions.matches;
import static androidx.test.espresso.matcher.ViewMatchers.isDisplayed;
import static androidx.test.espresso.matcher.ViewMatchers.withId;
import static androidx.test.espresso.matcher.ViewMatchers.withHint;

@LargeTest
@RunWith(AndroidJUnit4.class)
public class EnrollmentActivityTest {

    @Rule
    public ActivityTestRule<EnrollmentActivity> mActivityTestRule = new ActivityTestRule<>(EnrollmentActivity.class);

    @Test
    public void enrollmentActivityTest() {
        onView(withId(R.id.buttonContinue)).check(matches(isDisplayed()));
        onView(withId(R.id.buttonContinue)).perform(click());
        onView(withHint(R.string.password_username_placeholder)).perform(typeText("testlogin"));
        onView(withHint(R.string.password_password_placeholder)).perform(typeText("testpassword"));
    }

}
```
