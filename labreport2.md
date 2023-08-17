**A JUnit test and any associated code:**


```
#import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testReverseInPlace1() {
    int[] input1 = {0, 1, 2, 3, 4};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[] { 4, 3, 2, 1, 0}, input1);
  }

  @Test
  public void testReversed1() {
    int[] input1 = {0, 1, 2, 3, 4};
    assertArrayEquals(new int[] { 4, 3, 2, 1, 0}, ArrayExamples.reversed(input1));
  }

  @Test
  public void testAverageWithoutLowestMultipleLowestValues() {
    double[] inputArray = {2.0, 3.0, 4.0, 2.0, 2.0};
    double expectedAverage = (3.0 + 4.0) / 2; // Excluding all 2.0 values, then dividing by 2 (length of array minus count of lowest value)
    assertEquals(expectedAverage, ArrayExamples.averageWithoutLowest(inputArray), 0.001); // The third parameter is a delta for floating-point comparisons
}


}

```


**Screenshot:**
![Image](C:\Users\16267\OneDrive\Desktop\screenshot.png)


**Before:**

```
#// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

```


**After:**

```
#// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }

```

**Why the fix addresses the issue**

As the loop progresses, the original elements in the first half of the array are being overwritten, and by the time the loop tries to reverse the second half, 
those original values are already lost. Essentially, we're copying the reversed values of the first half of the array into the first half itself, losing the original values.




