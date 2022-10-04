# IshanSinbgla



<details>
<summary>Raj is a very smart kid (cyclic array)</summary>

```python
#include<bits/stdc++.h>
using namespace std;

int mod = 1e9+7;

int main() {
	int n;
	cin>>n;

	int sum = 0;	
	for(int i=0;i<n;i++){
		int x; cin >> x;
		sum += x;
		sum %= mod;
	}

    // total sum = ts
	int ts = sum;

	int q; cin >> q;
	for(int i=0;i<q;i++){
		int x ; cin>>x; // take the input but dont shift 
        // just add sum
		sum += ts;
        // and upadte it
		ts = sum;
		sum %= mod;
	}

	cout<<sum%mod<<endl;

	return 0;
}
```
	
</details>

<details>
<summary>Take as input N, the size of array.</summary>
	
```python
#include <iostream>
using namespace std;
int main() {
    int n,a[1000];
    int target;
    cin>>n;
    for(int i=0;i<n;i++)
    {
        cin>>a[i];
    }
    for(int i=0;i<n;i++)
    {
        for(int j = 0; j < n-i-1; j++)  
        {
           if (a[j] > a[j+1])
           { 
              int temp = a[j];
              a[j] = a[j+1];
              a[j+1] = temp;
           }
        }

    }
    cin>>target;
    for(int i=0;i<n-1;i++)
    {
        for(int j=i+1;j<n;j++)
        {
            for(int k=j+1;k<n;k++)
            {
                if(a[i]+a[j]+a[k]==target)
                {
                    cout<<a[i]<<", "<<a[j]<<" and "<<a[k]<<endl;
                }
            }
        }
    }

}
```
</details>
								
<details>
<summary>You are provided two sorted arrays</summary>
	
```python
#include <bits/stdc++.h>
using namespace std;
int maxsumpath(int arr[],int arr1[],int m,int n)
{
    int sum1 = 0,sum2= 0 ; 
    int res = 0 ; 
    int i=0,j=0;
    while(i<m&&j<n)
    {
        if(arr[i]>arr1[j])
        { sum2=sum2+arr1[j];
           j++; }
          else if(arr[i]<arr1[j])
          {
              sum1+=arr[i]; 
              i++;
          }
          else
          {
              if(sum1>=sum2)
              res=res+sum1 ; 
              else
              res=res+sum2 ;
              while(i<m&&j<n&&arr[i]==arr1[j])
              {
              res=res+arr[i] ; 
              i++; 
              j++; 
              }
              sum1=0 ; 
              sum2=0;
          }
     }
     while (i < m)
         sum1  +=  arr[i++];
     while (j < n)
         sum2 +=  arr1[j++];
     if(sum1>=sum2)
     res=res+sum1 ; 
     else
     res=res+sum2 ;
     
     
 
 return res ; 
}
int main() {
    int t;
    cin>>t;
    while(t>0)
    {
        int m ; 
        cin>>m;
        int n ; 
        cin>>n;
        int arr[m] ;  
        int arr1[n]; 
        for(int i=0;i<m  ;i++)
        {
            cin>>arr[i]; 
        }
        for(int j=0;j<n;j++)
        {
            cin>>arr1[j]; 
        }
        int ans = maxsumpath(arr,arr1,m,n); 
        cout<<ans<<endl;
        t-- ;
    }
    return 0;
}
```
</details>
								
<details>
<summary>Pair of roses problem</summary>
	
```python
#include<bits/stdc++.h>

    using namespace std;

    void PairOfRoses(int arr[], int n, int target){

        int i = 0;

        int j = n-1;

        int p,q;

        while(i<j){
            if(arr[i] + arr[j]>target){
            j--;
            } else if (arr[i] + arr[j]< target){
                i++;
            } else {

                p=arr[i];

                q=arr[j];

                i++;

                j--;

            }

        }

        cout<<"Deepak should buy roses whose prices are "<<p<<" and "<<q<<"."<<endl;

    }

    int main() {

        int t;

        cin>>t;

        while(t--){

            int n;

            cin>>n;

            int arr[n];

            for(int i =0;i<n;i++){

                cin>>arr[i];

            }

            sort(arr, arr+n);

            int target;

            cin>>target;

          PairOfRoses(arr, n, target);

        }

        return 0;

    }
```
</details>
								
<details>
<summary>Next Permutation</summary>
	
```python
#include<iostream>
#include<algorithm>
using namespace std;
int main() {int t;
cin>>t;
while(t--){
	int n;
cin>>n;
int arr[n];
for(int i=0;i<n;i++)
{
	cin>>arr[i];
}
int i=n-2,flag=0;
for(;i>=0;i--)
{
	if(arr[i]>=arr[i+1])
	continue;
	else
	{flag=1;break;}
}
sort(arr+i+1,arr+n);
if(flag)
{
	for(int j=i+1;j<n;j++)
	{if(arr[j]>arr[i])
	{swap(arr[i],arr[j]);break;}
}
}
for(int p=0;p<n;p++)
{
	cout<<arr[p]<<" ";
}cout<<endl;}
	return 0;                                                     
}
```
</details>
								
<details>
<summary>Max Circular sum</summary>
	
```python
#include<bits/stdc++.h>
using namespace std;

int kadane(int a[], int n);
int maxCircularSum(int a[], int n)
{
int max_kadane = kadane(a, n);

int max_wrap = 0, i;
for (i=0; i<n; i++)
{
        max_wrap += a[i];    
        a[i] = -a[i];       
}
max_wrap = max_wrap + kadane(a, n);

return (max_wrap > max_kadane)? max_wrap: max_kadane;
}

int kadane(int a[], int n)
{
    int max_so_far = 0, max_ending_here = 0;
    int i;
    for (i = 0; i < n; i++)
    {
        max_ending_here = max_ending_here + a[i];
        if (max_ending_here < 0)
            max_ending_here = 0;
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

int main()
{
    int t;
    cin>>t;
    for(int i=0;i<t;i++)
    {
       int n;
       cin>>n;
       int a[n];
       for(int j=0;j<n;j++)
       {
           cin>>a[j];
       }
        cout<< maxCircularSum(a, n) <<endl;
    }
    return 0;
}
```
</details>
								
<details>
<summary>Help Ramu</summary>
	
```python
#include<bits/stdc++.h>
using namespace std;
int mincost(int c1,int c2,int c3,int c4,int r,int c,int a[],int b[])
{
    int cost2=0,cost3,cost4,i;
    for(i=0;i<r;i++)
    {
        cost2+=min((a[i]*c1),c2);
    }
    cost3=min(cost2,c3);
    cost2=0;
    for(i=0;i<c;i++)
    {
        cost2+=min((b[i]*c1),c2);
    }
    cost3+=min(cost2,c3);
    cost4=min(cost3,c4);
    return cost4;
}
int main() {
    int t;
    int c1,c2,c3,c4,r,c;
    cin>>t;
    while(t--)
    {
        cin>>c1>>c2>>c3>>c4;
        cin>>r>>c;
        int a[r],b[c];
        for(int i=0;i<r;i++)
        {
            cin>>a[i];
        }
        for(int j=0;j<c;j++)
        {
            cin>>b[j];
        }
        int cost=mincost(c1,c2,c3,c4,r,c,a,b);
        cout<<cost<<"\n";
    }
	return 0;
}
```
</details>
								
<details>
<summary>Alex Goes Shopping</summary>
	
```python
#include<iostream>
using namespace std;
int main() {
    int n;
    cin>>n;
    int arr[n];
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    int q;
    cin>>q;
    while(q--){
        int amount, k;
        cin>>amount>>k;
        int cnt = 0;
        for(int i=0;i<n;i++){
            if(amount % arr[i] == 0){
                cnt++;
            }
        }
        if(cnt >= k){
            cout<<"Yes"<<endl;
        }
        else{
            cout<<"No"<<endl;
        }
    }
}
```
</details>
								
<details>
<summary>Product of Array Except Self</summary>
	
```python
#include <bits/stdc++.h>
#include <string>
using namespace std;
vector<string> summaryRanges(vector<int>&nums) {

 	int n = nums.size();
 	vector<string> ans;
 	int i = 0;

 	while(i < n){

 		string temp = "";
 		temp += to_string(nums[i]);
 		int num = nums[i];

 		while(i+1 < n && nums[i+1] == nums[i]+1){

 			i++;
 		}

 		if(nums[i] != num){
 			temp += "->";
 			temp += to_string(nums[i]);
 		}
 		ans.push_back(temp);
 		i++;
 	}
        return ans;
 }

int main()
{
	int n;
	cin>>n;
	vector<int> a;
	int data;

	for (int i = 0; i < n; i++)
	{
		cin>>data;
		a.push_back(data);
	}

vector<string> ans = summaryRanges(a);
for (int i = 0; i < ans.size(); i++)
{
	cout<<ans[i]<<' ';
}
	return 0;
}
```
</details>
								
<details>
<summary>ARRAYS-WAVE PRINT ROW WISE</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     int n,m;
     cin>>m>>n;

     int a[m][n],i,j;

     for(i=0;i<m;i++)
     {
          for(j=0;j<n;j++)
               cin>>a[i][j];
     }
     for(i=0;i<m;i++)
     {
          if(i%2==0)
          {
               for(j=0;j<n;j++)
                    cout<<a[i][j]<<", ";
          }
          else
          {
               for(j=n-1;j>=0;j--)
                    cout<<a[i][j]<<", ";
          }
     }
     cout<<"END";
}
```
</details>
								
<details>
<summary>ARRAYS-WAVE PRINT COLUMN WISE</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     int n,m;
     cin>>m>>n;

     int a[m][n],i,j;

     for(i=0;i<m;i++)
     {
          for(j=0;j<n;j++)
               cin>>a[i][j];
     }
     for(j=0;j<n;j++)
     {
          if(j%2==0)
          {
               for(i=0;i<m;i++)
                    cout<<a[i][j]<<", ";
          }
          else
          {
               for(i=m-1;i>=0;i--)
                    cout<<a[i][j]<<", ";
          }
     }
     cout<<"END";
}
```
</details>
								
<details>
<summary>Arrays-Spiral Print Anticlockwise</summary>
	
```python
#include<bits/stdc++.h>
using namespace std;

void spiral_print (int a[][1000] , int m, int n ) // need array, row and column
{

    int startRow = 0;
    int startCol = 0;
    int endRow = m - 1;
    int endCol = n - 1;

    while (startRow <= endRow && startCol <= endCol)
    {
        // Print the First Column

        for (int i = startRow; i <= endRow; i++)
        {

            cout << a[i][startCol] << ", ";

        }

        startCol ++ ;   // for next iteration... we have updated the columns

        for (int i = startCol; i <= endCol; i++)
        {

            cout << a[endRow][i] << ", ";

        }

        endRow-- ;

        // now print the last column

        if (endCol >= startCol)                  // this condition for all MATRIX

        {

            for (int i = endRow; i >= startRow; i--)
            {

                cout << a[i][endCol] << ", ";

            }

            endCol-- ;

            // now print the first row


        }


        if (endRow >= startRow)                // this condition for all MATRIX
        {


            for (int i = endCol; i >= startCol; i--)
            {

                cout << a[startRow][i] << ", ";

            }

            startRow++;


        }

    }
}

int main()
{

    int a[1000][1000];
    int m, n;
// cout << "Enter the number of rows : ";
    cin >> m;

// cout << "Enter the number of columns : ";
    cin >> n;

    for (int row = 0; row <= m - 1; row++)
    {

        for (int col = 0; col <= n - 1; col++)
        {

            cin >> a[row][col];

        }

        cout << endl;

    }

    cout << endl;


    spiral_print (a, m, n);

    cout << "END";


    return 0;
}
```
</details>
								
<details>
<summary>Matrix search</summary>
	
```python
#include <iostream>
using namespace std;
int main ()
{
    int m,n,o,i,j,arr[100][100];
    bool ans;
    cin>>m>>n;
    for(i=0;i<m;i++)
    for(j=0;j<n;j++)
    cin>>arr[i][j];
    cin>>o;
    i=0,j=n-1;
    ans=false;
    while(i<m&&j>=0)
    {
        if(o==arr[i][j])
        {
            ans=true;
            break;
        }
        else if(o<arr[i][j])
        j--;
        else if(o>arr[i][j])
        i++;
    }
    cout<<ans;
}
```
</details>
								
<details>
<summary>Strings-isPalindrome</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     string str;
     cin>>str;
     bool flag=true;
     for(int i=0;i<str.length()/2;i++)
     {
          if(str[i]!=str[str.length()-i-1])
          {
               flag=false;
               break;
          }
     }
     if(flag)
          cout<<"true";
     else
          cout<<"false";
}
```
</details>
								
<details>
<summary>Arrays-Spiral Print Clockwise</summary>
	
```python
#include <iostream>
using namespace std;

int main() {
    int m,n;
	cin>>m>>n;
    int sr=0,sc=0,ec=n-1,er=m-1;
    int arr[m][n];
    for(int i=0;i<m;i++){
        for(int j=0;j<n;j++){
            cin>>arr[i][j];
        }
    }

    while(sr<=er && sc<=ec){
        for(int col=sc;col<=ec;col++){
            cout<<arr[sr][col]<<", ";
        }
        sr++;
        for(int row=sr;row<=er;row++){
            cout<<arr[row][ec]<<", ";
        }
        ec--;
        if(sr<=er)
    {    for(int col=ec;col>=sc;col--){
            cout<<arr[er][col]<<", ";
        }

        er--;
    }
        if(sc<=ec){
        for(int row=er;row>=sr;row--){
            cout<<arr[row][sc]<<", ";
        }
        sc++;
        }
    }
    cout<<"END";
    return 0;
}
```
</details>
								
<details>
<summary>Strings-Count Palindromic Substrings</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int palindrome(int i,int j,string str)
{
     if(i==j)
          return 1;
     for(;i<=j;)
     {
          if(str[i]!=str[j])
               break;
          i++;j--;
     }
     if(i>j)
          return 1;
     else
          return 0;
}

int main()
{
     string str;
     cin>>str;
     int n=str.length();
     int i,j,count=0;
     for(i=0;i<n;i++)
     {
          for(j=i;j<n;j++)
          {
               if(palindrome(i,j,str)==1)
                    count++;
          }
     }
     cout<<count;
}
```
</details>
								
<details>
<summary>Rotate Image!</summary>
	
```python
#include<iostream>
#include<algorithm>
using namespace std;

void rotate1(int a[][1000],int n){
	for(int i=0;i<n;i++){
        reverse(a[i],a[i]+n);		
	}
	
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			if(i<j){
				swap(a[i][j],a[j][i]);
			}
		}
	}
	
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			cout<<a[i][j]<<" ";
		}
		cout<<endl;
	}
	
}

int main(){
	int arr[1000][1000],n;
	cin>>n;
	
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			cin>>arr[i][j];
		}
	}
	
	rotate1(arr,n);
	
	return 0;
}
```
</details>
								
<details>
<summary>Strings-Toggle Case</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     string str;
     cin>>str;

     for(int i=0;i<str.length();i++)
     {
          if(str[i]>=65&&str[i]<=90)
               str[i]+=32;
          else
               str[i]-=32;
          cout<<str[i];
     }
}
```
</details>
								
<details>
<summary>Strings-Odd Even Character</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     string str;
     cin>>str;

     for(int i=0;i<str.length();i++)
     {
          if(i%2==0)
               str[i]++;
          else
               str[i]--;
          cout<<str[i];
     }
}
```
</details>
								
<details>
<summary>Strings-String Compression</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int  main()
{
     string str;
     cin>>str;

     int count =1;
     char last_digit=str[0];
     cout<<last_digit;
     for(int i=1;i<str.length();i++)
     {
          if(str[i]==last_digit)
               count++;
          else if(count>1)
          {
               cout<<count;
               count=1;
               last_digit=str[i];
               cout<<last_digit;
          }
          else if(count==1)
          {
               last_digit=str[i];
               cout<<last_digit;
          }
     }
     if(count>1)
          cout<<count;
}
```
</details>
								
<details>
<summary>Strings-Difference in Ascii Codes</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

string convert(int t)
{
     ostringstream ss;
     ss<<t;
     return ss.str();
}

int main()
{
     string str;
     cin>>str;
     string str2="";
     bool flag=false;
     int i;
     for(i=0;i<str.length();)
     {
          if(flag==false)
          {
               str2+=str[i];
               flag=true;
               i++;
          }
          else
          {
               int x;
               x=str[i]-str[i-1];
               str2+=convert(x);
               flag = false;
          }
     }
     cout<<str2;
}
```
</details>
								
<details>
<summary>Strings-Max Frequency Character</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     string str;
     cin>>str;

     vector <int> a(127,0);

     int i,max=0,index;
     for(i=0;i<str.length();i++)
     {
          //cout<<str[i]-97<<"\n";
          a[str[i]]++;
     }
     for(i=0;i<127;i++)
     {
          if(a[i]>max)
          {
               index=i;
               max=a[i];
          }
     }
    // cout<<index<<"\n";
     string str2=" ";
     str2[0]+=index-32;
     cout<<str2;
}
```
</details>
								
<details>
<summary>Strings-Remove Duplicates</summary>
	
```python
#include<bits/stdc++.h>

using namespace std;

int main()
{
     string str;
     cin>>str;

     int i;
     for(i=0;i<str.length();i++)
     {
          if(i==0)
               cout<<str[i];
          else if(str[i]!=str[i-1])
                    cout<<str[i];
     }
}
```
</details>
								
<details>
<summary>Form Biggest Number</summary>
	
```python
#include<iostream>
using namespace std;
int main()
{
  int tc;
  cin>>tc;
  while(tc>0)
  {
    int n;
    cin>>n;
    string s[n];
    for(int i=0;i<n;i++)
    {
      cin>>s[i];
    }
    for(int i=0;i<n;i++)
    {
      for(int j=i+1;j<n;j++)
      {
        if(s[j]+s[i]>s[i]+s[j])
        {
          string b=s[j];
          s[j]=s[i];
          s[i]=b;
        }
      }
    }
    for(int i=0;i<n;i++)
      cout<<s[i];
    cout<<endl;
    tc--;
  }
  return 0;
}
```
</details>
								
<details>
<summary>String Compression</summary>
	
```python
#include<bits/stdc++.h> 
using namespace std; 
int main() 
{ 
    string s; 
    cin>>s; 
    if(s.length()==1)
    { 
        cout<<s<<"1"; 
        return 0; 
    } 
    for(int i=0;i<s.length();i++)
    { 
        int count=1; 
        for(int j=i+1;j<s.length();j++)
        { 
            if(s[i]==s[j]) 
            { count++; 
            } else
            { break; 
            } 
        } 
        cout<<s[i]<<count; 
        i=i+count-1; 
    } 
    return 0; 
} 
```
</details>
								
<details>
<summary>Finding CB Numbers</summary>
	
```python
#include<bits/stdc++.h>
using namespace std;
bool isCb(long long int s)
{  if(s==0 ||s==1)
    return false;
   int cb[]={2,3,5,7,11,13,17,19,23,29};
   for(int i=0;i<10;i++)
   {
       if(s==cb[i])
       {
           return true;
       }
   }
    for(int i=0;i<10;i++)
   {
       if(s%cb[i]==0)
       {
           return false;
       }
   }
return true;
}
bool isvalid(int *visited,string str,int start,int end)
{
    for(int i=start;i<end;i++)
    {
        if(visited[i]==1)
        {
            return false;
        }
    }
    return true;
}
int main()
{
    int n;
    cin>>n;
    string s;
    cin>>s;
    int visited[s.length()];
    for(int i=0;i<s.length();i++)
    {
        visited[i]=0;
    }
    int cnt=0;
    for(int i=1;i<=s.length();i++)
    {
        for(int j=0;j+i-1<s.length();j++)
        {
                string str=s.substr(j,i);
			
                if(isCb(stoll(str)) and isvalid(visited,str,j,j+i))
                {
                    cnt++;
                    for(int k=j;k<j+i;k++)
                    {
                        visited[k]=1;
                    }
                }
    
        }
    }
    cout<<cnt;
    return 0;
}
```
</details>
			
