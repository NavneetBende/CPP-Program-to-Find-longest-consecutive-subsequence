Longest Consecutive subsequence in C++
Here, in this page we will discuss the program to find the longest consecutive subsequence in C++ . We are Given with an array of integers, we need to find the length of the longest sub-sequence such that elements in the sub-sequence are consecutive integers, the consecutive numbers can be in any order.

Longest Consecutive subsequence
Method Discussed :
Method 1 : Brute Force
Method 2 : Using Hash-map
Method 3 : Using Priority Queue.
 

Method 1 (Brute force Approach) :
First sort the given input array.
Remove the multiple occurrences of elements, run a loop and keep a count and max (both initially zero).
Run a loop from 0 to N and if the current element is not equal to the previous (element+1) then set the count to 1 else increase the count.
Update max with a maximum of count and max.
 
Time and Space Complexity :
Time – complexity : O(n log n)
Space – complexity : O(1)
longest subsequence
Method 1 : code in C++
Run
#include <bits/stdc++.h>
using namespace std;

// Returns length of the longest
// contiguous subsequence
int findLongestConseqSubseq(int arr[], int n)
{
    int ans = 0, count = 0;

    // sort the array
    sort(arr, arr + n);

    vector<int> v;
    v.push_back(arr[0]);

    //insert repeated elements only once in the vector
    for (int i = 1; i < n; i++)
    {
        if (arr[i] != arr[i - 1])
        v.push_back(arr[i]);
    }
    // find the maximum length
    // by traversing the array
    for (int i = 0; i < v.size(); i++) { if (i > 0 && v[i] == v[i - 1] + 1)
            count++;
        // reset the count
        else
            count = 1;
        // update the maximum
        ans = max(ans, count);
    }
    return ans;
}

// Driver code
int main()
{

  int arr[]={1, 3, 2, 2};
  int n = sizeof(arr)/sizeof(arr[0]);


  cout << "Length of the Longest contiguous subsequence is "<< findLongestConseqSubseq(arr, n);
  return 0;
}
Output :
Length of the Longest contiguous subsequence is 3						
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Minimum no. of Jumps to reach the end of an array 

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 :
First we will create a hash-map.
Now, iterate over the array for every i-th element check if this element is the starting point of a subsequence. To check this, simply look for arr[i] – 1 in the hash, if not found, then this is the first element a subsequence.
If this element is the first element, then count the number of elements in the consecutive starting with this element. Iterate from arr[i] + 1 till the last element that can be found.
If the count is more than the previous longest subsequence found, then update this.
 
Time and Space Complexity :
Time – complexity : O(n)
Space – complexity : O(n)
Method 2 : Code in C++
Run
#include <bits/stdc++.h>
using namespace std;

int findLongestConseqSubseq(int arr[], int n)
{
  unordered_set<int> S;
  int ans = 0;

  // Hash all the array elements
  for (int i = 0; i < n; i++)
   S.insert(arr[i]);

  // check each possible sequence from
  // the start then update optimal length
  for (int i = 0; i < n; i++) { 
   if (S.find(arr[i] - 1) == S.end()) { 
    int j = arr[i]; 
    while (S.find(j) != S.end())
          j++; 
    ans = max(ans, j - arr[i]); 
  }
 } 
return ans;
 } 
  // Driver code 
  int main() { 

   int arr[] = {1, 3, 2, 2};
   int n=sizeof(arr)/sizeof(arr[0]);
   cout << "Length of the Longest contiguous subsequence is "<< findLongestConseqSubseq(arr, n);
   return 0;
}
Output :
Length of the Longest contiguous subsequence is 3						
Method 3 :
In this method we will use priority queue.

Create a Priority Queue to store the element
Store the first element in a variable.
Remove it from the Priority Queue.
Check the difference between this removed first element and the new peek element
If the difference is equal to 1 increase count by 1 and repeats step 2 and step 3
If the difference is greater than 1 set counter to 1 and repeat step 2 and step 3
if the difference is equal to 0 repeat step 2 and 3
if counter greater than the previous maximum then store counter to maximum
Continue step 4 to 7 until we reach the end of the Priority Queue
Return the maximum value
 
Time and Space Complexity :
Time – complexity : O(n logn)
Space – complexity : O(n)
Method 3 : Code in C++
Run
#include <bits/stdc++.h>
using namespace std;
int findLongestConseqSubseq (int arr[], int N)
{
    priority_queue<int, vector<int>, greater <int> >pq;  
    for (int i = 0; i < N; i++)
    {
      // adding element from           
      // array to PriorityQueue           
      pq.push (arr[i]);

    }
  int prev = pq.top ();
  pq.pop ();
  // Taking a counter variable with value 1     
  int c = 1;
  // Storing value of max as 1    
  // as there will always be   
  // one element    
  int max = 1;
  while (!pq.empty ())
    {
      if (pq.top () - prev < 1)
	{
	  // Store the value of counter to 1
	  // As new sequence may begin
	  c = 1;
	  // Update the previous position with the
	  // current peek And remove it
	  prev = pq.top ();
	  pq.pop ();
	}

      // Check if the previous
      // element and peek are same
      else if (pq.top () - prev == 0)
	{
	  // Update the previous position with the
	  // current peek And remove it
	  prev = pq.top ();
	  pq.pop ();
	}

      // If the difference
      // between previous element and peek is 1
      else
	{

	  // Update the counter
	  // These are consecutive elements
	  c++;

	  // Update the previous position
	  // with the current peek And remove it
	  prev = pq.top ();
	  pq.pop ();
	}

      // Check if current longest
      // subsequence is the greatest
      if (max < c)
	{

	  // Store the current subsequence count as
	  // max
	  max = c;
	}
    }
  return max;
}

// Driver code
int
main ()
{

  int arr[] = { 1, 3, 2, 2 };
  int n = sizeof (arr) / sizeof (arr[0]);
  cout << "Length of the Longest contiguous subsequence is " << findLongestConseqSubseq (arr, n);
  return 0;
}
Output :
Length of the Longest contiguous subsequence is 3						
Prime Course Trailer

Related Banners
Get PrepInsta Prime & get Access to all 200+ courses offered by PrepInsta in One Subscription

Get Prime
While loop in C
