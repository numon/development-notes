# Espresso

There are 6 types of annotations that can be applied to the methods used inside the test class,which are @Test, @Before, @BeforeClass, @After, @AfterClass, @Rule
![Hooks](images/hook.jpeg)

Important things to note is that:

The activity will be launched using the @Rule before test code begins
By default the rule will be initialised and the activity will be launched(onCreate, onStart, onResume) before running every @Before method
Activity will be Destroyed(onPause, onStop, onDestroy) after running the @After method which in turn is called after every @Test Method
The activity’s launch can be postponed by setting the launchActivity to false in the constructor of ActivityTestRule ,in that case you will have to manually launch the activity before the tests

## Machers

![Hooks](images/matchers.png)
Espresso uses onView (Matcher<View> viewMatcher) method to find a particular view among the View hierarchy. onView() method takes a Matcher as argument. Espresso provides a number of these ViewMatchers which can be found in this Espresso Cheat sheet.

Every UI element contains properties or attributes which can be used to find the element.Suppose for finding an element with

`android:id=“+id/login_button”`
We can write

`Espresso.onView(withId(R.id.login_button))`
