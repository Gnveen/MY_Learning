// prg to palindrome with out revering array
#include <stdio.h>
int isPalindrome(int arr[], int size) {
    // Compare elements from both ends towards the center
    for (int i = 0; i < size / 2; i++) {
        if (arr[i] != arr[size - i - 1]) {
            return 0; // Not a palindrome
        }
    }
    return 1; // Is a palindrome
}
int main() {
    int arr[] = {1, 2,4, 3, 2, 1};
    int size = sizeof(arr) / sizeof(arr[0]);
    if (isPalindrome(arr, size)) {
        printf("The array is a palindrome.\n");
    } else {
        printf("The array is not a palindrome.\n");
    }
    return 0;
}

// finding non-reperting element without iteration

//find reperting element without iteration

// printing array with out loop
#include <stdio.h>
void printArray(int *arr, int size) {
    if (size <= 0) return;  // Base case
    printf("%d ", *arr);    // Print current element
    printArray(arr + 1, size - 1); // Recursive call for the next element
}
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    printArray(arr, size);
    return 0;
}
//shorting array with O(n)
#include <stdio.h>
#define MAX 100 
int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int size = sizeof(arr)/sizeof(arr[0]);
    int count[MAX + 1] = {0}; // Initialize count array
    // Count occurrences of each number
    for (int i = 0; i < size; i++) 
        count[arr[i]]++;
    // Print sorted array
    printf("Sorted array: ");
    for (int i = 0; i <= MAX; i++) 
        while (count[i]-- ) 
            printf("%d ", i);
    return 0;
}

#include<stdio.h>
#include<string.h>
/*
int main()
// declaration of varibles 
{ int a[6]={{1,3},
            {2,4},
            {5},};
   //scanf("%d",&a);
    printf("%d\n",a);
    //char *b[5]={'a','b','c','d','e'};
    //printf("%c\n",b);
}*/

//int main()
/*{   int s,r,i;
    scanf("%d ",&r);
    scanf("%d ",&s);
    char a[s];
    char b[r];
    scanf("%s",&a);
    scanf("%s",&b);
    printf("%s %s",a,b);
}*/
 
/*int main()
{
    int a[5] = {2, 3};
    printf("%d, %d, %d\n", a[2], a[3], a[4]);
    return 0;  //o/p is   0,0,0. When an automatic array is partially initialized, the remaining elements are initialized to 0
}*/
// reversing the array
 /*{
    int a[20],i,n;
    scanf("%d",&n);// array size
    for(i=0;i<n;i++)// i/p
    {
        printf("Enter the no.:");
        scanf("%d",&a[i]);
    }
    for(i=0;i<n;i++)//  o/p
    {
        printf("normal order%d\n",a[i]);
    }
    for(i=n-1;i>=0;i--)
    {
        printf("revers order%d\n",a[i]);
    }
         // Store and display the array in reverse order
    int arr[n]; // Define the reverse array of the same size
    printf("Array in reverse order:\n");
    for (int j = 0; j < n; j++) {
        arr[j] = array[n - 1 - i]; // Fill the reverse array
        printf("%d ", arr[i]);     // Print the reversed array elements
    }
}*/
// sum of all the elements
/*{
    int a[20],i,n,s;
    scanf("%d",&n);// array size
    for(i=0;i<n;i++)// i/p
    {
        printf("Enter the no.:");
        scanf("%d",&a[i]);
    } 
    for(i=0;i<n;i++)//  o/p
    {
        s=s+a[i];
        
    } printf("sum %d\n",s);
    }*/
// coping elements
 /*{
    int a[20],i,j,n;
    scanf("%d",&n);// array size
    for(i=0;i<n;i++)// i/p
    {
        printf("Enter the no.:");
        scanf("%d",&a[i]);
    }
    for(i=0;i<n;i++)//  o/p
    {
        a[j]=a[i];  // coping i array elements to j array
        printf("copied %d\n",a[j]);
    }
}*/

// finding how many times a duplicate number is repeted
#include <stdio.h>
int main() {
    int ar[] = {1, 2, 3, 4, 1, 1,8, 3, 2, 2, 3, 2, 2}; // Sample array
    int size = sizeof(ar) / sizeof(ar[0]); // Calculate size of the array
    int freq[size]; // Array to store frequencies
    int i, j;
    // Initialize frequency array with 0
    for (i = 0; i < size; i++) {
        freq[i] = 0;    }
    // Count frequencies of each element
    for (i = 0; i < size; i++) {
        int count = 1;
        for (j = i + 1; j < size; j++) {
            if (ar[i] == ar[j]) {
                count++;
                freq[j] = -1; // Mark duplicate elements as -1
            }  }
        if (freq[i] != -1) {
            freq[i] = count; // Store the frequency
        }    }
    // Display frequencies of each element
    printf("Element | Frequency\n");
    for (i = 0; i < size; i++) {
        if (freq[i] != -1) {
            printf("   %d    |    %d\n", ar[i], freq[i]);
            } }
    return 0; }

// most repeating element

#include <stdio.h>
int main() {
    int ar[] = {1, 2, 3, 4, 1, 1, 3, 2, 2, 3, 2, 2}; // Sample array
    int size = sizeof(ar) / sizeof(ar[0]); // Calculate size of the array
    int freq[size]; // Array to store frequencies
    int i, j;
    // Initialize frequency array with 0
    for (i = 0; i < size; i++) {
        freq[i] = 0;
    }
    // Count frequencies of each element
    for (i = 0; i < size; i++) {
        int count = 1;
        for (j = i + 1; j < size; j++) {
            if (ar[i] == ar[j]) {
                count++;
                freq[j] = -1; // Mark duplicate elements as -1
            }       }
        if (freq[i] != -1) {
            freq[i] = count; // Store the frequency
        }    }
    // Find the element with the highest frequency
    int maxFreq = 0;
    int mostRepeatedElement = ar[0];
    for (i = 0; i < size; i++) {
        if (freq[i] > maxFreq) {
            maxFreq = freq[i];
            mostRepeatedElement = ar[i];
        }    }
    // Display the result
    printf("Element repeated most times: %d\n", mostRepeatedElement);
    printf("Number of repetitions: %d\n", maxFreq);

    return 0;
}

 // deleting dublicate elements  
 /*#include <stdio.h>
#include <string.h>
int main() {
    int sz = 10; // Define the maximum size of the array
    char a[sz];
    int i, j, k, n;
    // Input the string
    printf("Enter the string (max %d characters): ", sz - 1);
    scanf("%s", a);
    printf("Input = %s\n", a);
    // Get the length of the string
    n = strlen(a);
    // Outer loop to traverse the string
    for (i = 0; i < n - 1; i++) {
        for (k = i + 1; k < n; k++) {
            // Check for duplicate characters
            if (a[i] == a[k]) {
                // Shift elements to remove the duplicate
                for (j = k; j < n; j++) {
                    a[j] = a[j + 1];                }
                n--; // Reduce the length of the string
                k--; // Recheck the current position after shifting
            }
        }
    }
    // Terminate the modified string properly
    a[n] = '\0';
    // Print the result
    printf("Output = %s\n", a);
    return 0;


/*
// C Program to create multidimensional dimenctional array
#include <stdio.h>

int main()
{

	// creating 2d array
	int arr2d[2][2] = { 1, 2, 3, 4 };

	// creating 3d array
	int arr3d[2][2][2] = { 1, 2, 3, 4, 5, 6, 7, 8 };

	printf("2D Array: ");
	// printing 2d array
	for (int i = 0; i < 2; i++) {
		for (int j = 0; j < 2; j++) {
			printf("%d ", arr2d[i][j]);
		}
	}

	printf("\n3D Array: ");
	// printing 3d array
	for (int i = 0; i < 2; i++) {
		for (int j = 0; j < 2; j++) {
			for (int k = 0; k < 2; k++) {
				printf("%d ", arr3d[i][j][k]);
			}
		}
	}

	return 0;
}*/

/*
// size of array
int main()
{
	int x[10],y[3][4],z[2][3][5];
	printf("%u\t%u\t%u\t",sizeof(x),sizeof(y),sizeof(z));
}

// sum of elements
// 1st way
#include<stdio.h>
int main()
{
	int arr[5]={5,10,15,20,25};
	func(arr);
}
void func(int arr[])
{
	int i=5,sum=0;
	while(i>2)
		sum=sum+arr[--i];
	printf("sum=%d\n",sum);
}
// 2nd way
int main()
{
	int i=0,j=0,arr[6]={4,2,6,0,5,10};
	while(arr[i])
	{
		j+=arr[i];
		i++;
	}
	printf("j=%d\n",j);
}
// 3rd way 
int main()
{
	int i=3,j=0,arr[4]={2,4,8,16};
	while(i)
	{
		j+=arr[i];
		i--;
	}
	printf("j=%d\n",j);
}*/

/*
// swaping 2 arrays
int main() {
    int arr[] = {1, 2, 3, 4, 5, 6};
    int arr1[] = {7, 8, 9, 10, 11, 12};
    int size = sizeof(arr) / sizeof(arr[0]);
    printf("Before swapping:\n");
    printf("arr: ");
    for (int i = 0; i < size; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\narr1: ");
    for (int i = 0; i < size; i++)
    {
        printf("%d ", arr1[i]);
    }
    printf("\n");
    for (int i = 0; i < size; i++)
    {
        int temp = arr[i];
        arr[i] = arr1[i];
        arr1[i] = temp;
    }
    printf("\nAfter swapping:\n");
    printf("arr: ");
    for (int i = 0; i < size; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\narr1: ");
    for (int i = 0; i < size; i++)
    {
        printf("%d ", arr1[i]);
    }
    printf("\n");
    return 0;
}*/

//array and pointer 
/*int main()
{
   int arr[]={10,20,30};
    int *ptr;
    ptr=arr;
    printf("%d",*++ptr,*++ptr);
    printf("\n%d\n",*ptr++);
}*/

/*
// adding a element 
int main()
{
    int arr[100], n, new_element, position, i;
    // Input the size of the array
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    // Input the elements of the array
    printf("Enter the elements of the array:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    // Input the new element and position
    printf("Enter the element to be added: ");
    scanf("%d", &new_element);
    printf("Enter the position (1 to %d): ", n + 1);
    scanf("%d", &position);
    // Validate position input
    if (position < 1 || position > n + 1)
    {
        printf("Invalid position!\n");
        return 1; // Exit with error code
    }
    // Shift elements to the right to create space for the new element
    for (i = n; i >= position; i--)
    {
        arr[i] = arr[i - 1];
    }
    // Insert the new element
    arr[position - 1] = new_element;
    n++; // Increase the size of the array
    // Print the updated array
    printf("Array after adding the new element:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}  */
// adding element based on position 



// deleting a elemenrt
/*
int main()
{
    int arr[100], n, position, i;
    // Input the size of the array
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    // Input the elements of the array
    printf("Enter the elements of the array:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    // Input the position of the element to delete
    printf("Enter the position (1 to %d) of the element to be deleted: ", n);
    scanf("%d", &position);
    // Validate position input
    if (position < 1 || position > n)
    {
        printf("Invalid position!\n");
        return 1; // Exit with error code
    }
    // Shift elements to the left to overwrite the element at the specified position
    for (i = position - 1; i < n - 1; i++)
    {
        arr[i] = arr[i + 1];
    }
    n--; // Decrease the size of the array

    // Print the updated array
    printf("Array after deleting the element:\n");
    for (i = 0; i < n; i++) 
    {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0; // Program termination
}
*/
/*
// deleting based on value
int main()
{
    int arr[100], n, value, i, j, found = 0;
    // Input the size of the array
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    // Input the elements of the array
    printf("Enter the elements of the array:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }
    // Input the value to delete
    printf("Enter the value to delete: ");
    scanf("%d", &value);
    // Search for the value in the array
    for (i = 0; i < n; i++)
    {
        if (arr[i] == value)
        {
            found = 1;
            // Shift elements to the left to remove the value
            for (j = i; j < n - 1; j++)
            {
                arr[j] = arr[j + 1];
            }
            n--; // Decrease the size of the array
            i--; // Adjust index to account for shifted elements
        }
    }
    // Check if the value was found
    if (!found)
    {
        printf("Value not found in the array.\n");
    }
    else
    {
        // Print the updated array
        printf("Array after deleting the value:\n");
        for (i = 0; i < n; i++)
        {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }

    return 0;
}*/
/*
//shorting
#include <stdio.h>

int main()
{
    int arr[100], n, i, j, temp;

    // Input the size of the array
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);

    // Input the elements of the array
    printf("Enter the elements of the array:\n");
    for (i = 0; i < n; i++)
    {
        scanf("%d", &arr[i]);
    }

    // Bubble Sort algorithm for sorting in ascending order
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1]) // Compare adjacent elements
            {
                // Swap elements if they are out of order
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    // Print the sorted array
    printf("Array sorted in ascending order:\n");
    for (i = 0; i < n; i++)
    {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}*/
// Quick short
/*
#include <stdio.h>
int partition();
void quickSort(int arr[], int low, int high) {
    if (low > high) {
        int pivot = partition(arr, low, high);
        quickSort(arr, low, pivot - 1);
        quickSort(arr, pivot + 1, high);
    }
}
o                                          
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    quickSort(arr, 0, n - 1);

    printf("Sorted array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}*/
/*
// merging 2 arrays
int main()
{
    int arr1[50], arr2[50], merged[100];
    int n1, n2, n3, i, j;

    // Input the size and elements of the first array
    printf("Enter the number of elements in the first array: ");
    scanf("%d", &n1);
    printf("Enter the elements of the first array:\n");
    for (i = 0; i < n1; i++)
    {
        scanf("%d", &arr1[i]);
    }

    // Input the size and elements of the second array
    printf("Enter the number of elements in the second array: ");
    scanf("%d", &n2);
    printf("Enter the elements of the second array:\n");
    for (i = 0; i < n2; i++)
    {
        scanf("%d", &arr2[i]);
    }

    // Merge the two arrays
    n3 = n1 + n2; // Total size of the merged array
    for (i = 0; i < n1; i++)
    {
        merged[i] = arr1[i]; // Copy elements from the first array
    }
    for (j = 0; j < n2; j++, i++)
    {
        merged[i] = arr2[j]; // Copy elements from the second array
    }

    // Print the merged array
    printf("Merged array:\n");
    for (i = 0; i < n3; i++)
    {
        printf("%d ", merged[i]);
    }
    printf("\n");

    return 0;
}*/
// largest no
    /*int largest_element(int arr[], int num) 
{
    int i, max_element;
    max_element = arr[0]; // Initialize max_element with the first element

    for (i = 1; i < num; i++) 
    {
        if (arr[i] > max_element) 
            max_element = arr[i]; // Update max_element if a larger element is found
    }
    return max_element; // Return the largest element after the loop completes
}
int main() 
{   
    int arr[] = {1, 24, 15, 20, 55, -11, 30};
    int n = sizeof(arr) / sizeof(arr[0]); // Calculate the size of the array

    printf("Largest element of array is %d\n", largest_element(arr, n)); 

    return 0; // Return statement for successful execution
}*/

// Array multiplication in matrix
/*#include <stdio.h>

int main() {
    int i, j;
    // Define and initialize the matrices
    int a[3][3] = { {1, 2, 3},{4,5,1},{2,3,4 }};
    int b[3][3] = { {5,1,2},{3,4,5},{1,2,3}};
    int c[3][3];
    // Traverse the matrix 'a' and print its elements
    printf("Elements of matrix 'a':\n");
    // for (i = 0; i < 2; i++) { 
    //     for (j = 0; j < 5; j++) { 
    //         printf("a[%d][%d] = %d\n", i, j, a[i][j]); 
    //          printf("b[%d][%d] = %d\n", i, j, b[i][j]);
    //     }   }
        
         for (i = 0; i < 3; i++) { 
        for (j = 0; j < 3; j++) { 
            for(int k=0;k<3;k++){
           c[i][j]+= a[i][k]*b[k][j];
            }
        }  
         }
         for(i=0;i<3;i++){
             for(j=0;j<3;j++){
                      printf("c[%d][%d] = %d\n", i, j, c[i][j]);
             }
             
         }
      
         
    return 0;
}*/
// searching num of times element present 
/*
#include <stdio.h>
int main() {
    int i, j,b,count=0;
    // Define and initialize the matrices
    int a[9]={3,3,2,1,4,4,4,5,6};
    scanf("%d",&b);
    for(int i=0;i<9;i++){
        if(a[i]==b){
            count++;
        }
            }
    printf("%d",count);
    return 0;
}*/
/*
#include <stdio.h>
int main() {
    int ar[10] = {1, 2, 3, 4, 5, 6, 6};
    int n, pos;
    int s = sizeof(ar) / sizeof(ar[0]);
    printf("Enter the number to insert: ");    scanf("%d", &n);

    printf("Enter the position to insert at (0-based index): "); scanf("%d", &pos);
    // Ensure position is valid
    if (pos < 0 || pos > s) {
        printf("Invalid position!\n");
        return 1;    }
    int arr[s + 1];
    for (int i = 0, j = 0; i <= s; i++, j++) {
        if (i == pos) {
            arr[i] = n;
            j--; // Don't advance j, since we still need to copy ar[j] into arr[i+1] next
        } else {
            arr[i] = ar[j];
        }    }

    printf("Array after insertion: ");
    for (int i = 0; i <= s; i++) {
        printf("%d ", arr[i]);
    }

    return 0;
}*/