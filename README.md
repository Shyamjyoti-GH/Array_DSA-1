# Array_DSA-1

Finding Largest element of an Array:
## Brute Force TC= O(n logn)
    int largestElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        return nums[nums.size()-1];
    }
## Optimal solution TC= O(n)
    int largestElement(vector<int>& nums) {
        int largest= nums[0];
        for(int i=1; i<nums.size(); i++){
            if(largest < nums[i]) largest= nums[i];
        }
        return largest;
    }

Second Largest element in an Array without sorting:
## Brute Force TC= O(n)
    int secondLargestElement(vector<int>& nums) {
        int largest = nums[0];
        
        // First pass: find largest
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > largest)
                largest = nums[i];
        }
        
        int second = INT_MIN;
        // Second pass: find second largest
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] < largest && nums[i] > second)
                second = nums[i];
        }
        
        return (second == INT_MIN) ? 0 : second;
    }
## Optimal solution TC= O(n)
    int secondLargestElement(vector<int>& nums) {
        int first = INT_MIN, second = INT_MIN;
        for (int num : nums) {
            if (num > first) {
                second = first;
                first = num;
            } else if (num > second && num < first) {
                second = num;
            }
            return (second == INT_MIN) ? -1 : second;
        }
    }

To check if Array is sorted:
## Brute Force / Optimal solution TC= O(n)
    bool isSorted(vector<int>& nums){
        //your code goes here
        for(int i=0; i<nums.size()-1; i++){
            if(nums[i] > nums[i+1]) return false;
        }
        return true;
    }
Remove Duplicates  from a sorted array:
## Brute Force TC= O(n^2) SC=O(1)
    int removeDuplicates(vector<int>& nums) {
        if(nums.empty()) return 0;
        for(int i=0;i<nums.size()-1;){
            if(nums[i] == nums[i+1]){
                nums.erase(nums.begin() + i);
            }
            else i++;
        }
        return nums.size();
    }
## Average Case TC= O(n logn) SC= O(n)
    int removeDuplicates(vector<int>& nums) {
        set<int> st;
        for(int i=0; i<nums.size(); i++){
            st.insert(nums[i]);
        }
        int idx=0;
        for(auto it: st){
            nums[idx]= it;
            idx++;
        }
        return idx;
    }
## Optimal solution TC= O(n)
    int removeDuplicates(vector<int>& nums) {
        int i=nums[0];
        int idx=1;
        for(int j=1; j<nums.size(); j++){
            if(nums[j] != i){
                nums[idx]=nums[j];
                i= nums[j];
                idx++;
            } 
        }
        return idx;
    }

Left Rotate an Array by One place:
## Brute Force/ Optimal solution TC=O(n)
    void rotateArrayByOne(vector<int>& nums) {
        int temp= nums[0];
        for(int i=1; i<nums.size(); i++){
            nums[i-1]= nums[i];
        }
        nums[nums.size()-1]= temp;
    }

Left Rotate an Array by D places:
## Brute Force TC= O(n+d) SC= O(d)
    void rotateArray(vector<int>& nums, int d) {
        d= d % nums.size();
        vector<int>temp;
        for(int i=0; i<d; i++){
            temp.push_back(nums[i]);
        }
        for(int i=d; i<nums.size(); i++){
            nums[i-d]= nums[i];
        }
        int j=0;
        for(int i=nums.size()-d; i<nums.size(); i++){
            nums[i]= temp[j];
            j++;
        }    
    }
        //we can also change the last for loop directly into this
        
    for(int i=nums.size()-d; i<nums.size(); i++){
            nums[i]= temp[i-(nums.size()-d)];
        }
## Optimal solution TC= O(2n) SC= O(1)
    void rotateArray(vector<int>& nums, int d) {
        if(nums.size() == 0) return;
        d= d % nums.size();
        reverse(nums.begin(), nums.begin()+d);
        reverse(nums.begin()+d, nums.end());
        reverse(nums.begin(), nums.end());
    }
    //if asked to write reverse without using STL
    void reverse(int arr[], int start, int end){
        while(start <= end){
            int temp= arr[start];
            arr[start]= arr[end];
            arr[end]= temp;
            start++;
            end--;
        }
    }
    
Move Zeroes to End:
## Brute Force Tc= O(2n) SC= O(n)
    void moveZeroes(vector<int>& nums) {
        vector<int> temp;
        for(int i=0; i<nums.size(); i++){
            if(nums[i]) temp.push_back(nums[i]);
        }
        for(int i=0; i<temp.size(); i++){
            nums[i]= temp[i];
        }
        for(int i=temp.size(); i<nums.size(); i++){
            nums[i]=0;
        }
    }
## Optimal solution TC = O(n) SC= O(1)
    vector moveZeroes(vector<int>& nums) {
        int j=-1;
        for(int i=0; i<nums.size(); i++){
            if(nums[i] == 0) j = i;
            break;
        }
        if(j == -1) return nums;
        for(int i=j+1; i<n; i++){
            if(nums[i]) swap(nums[j], nums[i]);
            j++;
        }
    }

Linear Search:
Means search the element in the array and return the front most index where element is present if absent return -1

    int LinearSearch(vector<int>& nums, int no){
        for(int i=0; i<nums.size(); i++){
            if(nums[i] == no) return i;
        }
        return -1;
    }

Find the Union of two sorted Array:
## Brute Force TC= O(n+m) log(n+m) SC= O(n+m)
    vector<int> unionArray(vector<int>& nums1, vector<int>& nums2) {
        set<int> st;
        for(int i=0; i<nums1.size(); i++){
            st.insert(nums1[i]);
        }
        for(int i=0; i<nums2.size(); i++){
            st.insert(nums2[i]);
        }
        vector<int> unionVec;
        for(auto it: st){
            unionVec.push_back(it);
        }
        return unionVec;
    }
## Optimal solution TC= O(n+m) SC= O(n+m)
    vector<int> unionArray(vector<int>& nums1, vector<int>& nums2) {
    int n1 = nums1.size();
    int n2 = nums2.size();
    int i = 0, j = 0;
    vector<int> unionVec;

    while(i < n1 && j < n2) {
        if(nums1[i] < nums2[j]) {
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
        }
        else if(nums1[i] > nums2[j]) {
            if(unionVec.empty() || unionVec.back() != nums2[j]) {
                unionVec.push_back(nums2[j]);
            }
            j++;
        }
        else {  
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
            j++;
        }
    }
    //lets say one of the array got exhausted and other remains
        while(i < n1) {
            if(unionVec.empty() || unionVec.back() != nums1[i]) {
                unionVec.push_back(nums1[i]);
            }
            i++;
        }
        while(j < n2) {
            if(unionVec.empty() || unionVec.back() != nums2[j]) {
                unionVec.push_back(nums2[j]);
            }
            j++;
        }

        return unionVec;
    }

Find the Missing Number in an Array:
## Brute Force TC = O(n * m)
    int missingNumber(vector<int>& nums) {
        for(int i=0; i<=nums.size(); i++){
            bool found= false;
            for(int j=0; j<nums.size(); j++){
                if(nums[j] == i) {
                    found= true;
                    break;
                }
            }
            if(!found) return i;
        }
        return -1;
    }
## Average Solution TC= O(n) SC= O(n)
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        vector<int> hash(n+1, 0); // presence array

        for (int i = 0; i < n; i++) {
            hash[nums[i]] = 1;
        }

        for (int i = 0; i <= n; i++) {
            if (hash[i] == 0) return i;
        }

        return -1; 
    }
## Optimal Solution TC= O(n) SC= O(1)
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int sum = (n * (n + 1)) / 2; 
        int s2 = 0;
        for (int i = 0; i < n; i++) {
            s2 += nums[i];
        }
        return sum - s2;
    }

    //Optimal solution Through XOR
    
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int xor1 = 0, xor2 = 0;

        // XOR of 1 to n
        for (int i = 1; i <= n; i++) {
            xor1 = xor1 ^ i;
        }

        // XOR of all elements in nums
        for (int i = 0; i < n; i++) {
            xor2 = xor2 ^ nums[i];
        }

        // Missing number
        return xor1 ^ xor2;
    }
Maximum Consecutive Ones
## Optimal Solution TC= O(n) 
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int maxi=0;
        int count=0;
        for(int i=0; i<nums.size(); i++){
            if(nums[i] == 1){
                count++;
                maxi= max(maxi, count);
            }
            else count=0;
        }
        return maxi;
    }
Find the number that appears Twice and others once
## Brute Force TC= O(n^2)
    int singleNumber(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            int count = 0;
            for (int j = 0; j < nums.size(); j++) {
                if (nums[j] == nums[i]) count++;
            }
            if (count == 1) return nums[i];
        }
        return -1; 
    }
## Average Solution TC= O(n) SC= O(max value in array)
    int singleNumber(vector<int>& nums) {
        int maxi = nums[0];
        for (int i = 0; i < nums.size(); i++) {
            maxi = max(maxi, nums[i]);
        }
        
        vector<int> hash(maxi + 1, 0);
        
        for (int i = 0; i < nums.size(); i++) {
            hash[nums[i]]++;
        }
        
        for (int i = 0; i < nums.size(); i++) {
            if (hash[nums[i]] == 1) return nums[i];
        }
        
        return -1; /
    }
## Optimised solution TC= O(N) SC= O(1)
    //using Maps
    int singleNumber(vector<int>& nums) {
        map<int,int> mpp;
        for (int i = 0; i < nums.size(); i++) {
            mpp[nums[i]]++;
        }
        for (auto it : mpp) {
            if (it.second == 1) return it.first;
        }
        return -1;
    }
    //using XOR 
    int singleNumber(vector<int>& nums){
        int xorr= 0;
        for(int i=0; i<nums.size(); i++){
            xorr = xorr ^ nums[i];
        }
        return xorr;
    }
Longest SubArray with given Sum K (positives)
## Brute Force TC= O(n^2)
    int longestSubarrayBruteForce(vector<int>& nums, long long k) {
        int n = nums.size();
        int maxlen = 0;
        for (int i = 0; i < n; i++) {
            long long sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum == k) {
                    maxlen = max(maxlen, j - i + 1);
                }
            }
        }
        return maxlen;
    }
## Average Approach TC= O(n logn) SC= O(n)            //the Brute force and this Average one is for +ve and 0s
    int longestSubarray(vector<int> &nums, long long k) {
        map<long long, int> mpp;  
        long long sum = 0;
        int maxlen = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            if (sum == k) {
                maxlen = max(maxlen, i + 1);
            }
            long long rem = sum - k;
            if (mpp.find(rem) != mpp.end()) {
                int len = i - mpp[rem];
                maxlen = max(maxlen, len);
            }
            if (mpp.find(sum) == mpp.end()) {
                mpp[sum] = i;
            }
        }
        return maxlen;
    }
## Optimal Approach TC= O(n) SC= O(1)            //this one is for both +ve and -ve numbers
    int longestSubarray(vector<int> &nums, long long k){
        int left=0, right=0;
        long long sum= nums[0];
        int maxlen= 0;
        int n= nums.size();
        while(right<n){
            while(left<=right && sum>k){
                sum-= nums[left];
                left++;
            }
            if(sum == k){
                maxlen= max(maxlen, right-left+1);
            }
            right++;
            if(right<n) sum+=nums[right];
        }
        return maxlen;
    }
Two Sum
## Brute Force TC= O(n^2)
    vector<int> twoSum(vector<int>& nums, int target) {
        int n= nums.size();
        for(int i=0; i<n; i++){
            for(int j=i+1; j<n; j++){
                if(target == nums[i]+nums[j]){
                    return {i,j};
                }
            }
        }
        return {};
    }
## Average Approach TC= O(n logn) SC= O(n)
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> mpp; // or unordered_map for O(1) average
        int n = nums.size();

        for (int i = 0; i < n; i++) {
            int f = target - nums[i];
            if (mpp.find(f) != mpp.end()) {
                return {mpp[f], i};
            }
            mpp[nums[i]] = i;
        }
        return {};
    }
## Optimal Approach TC= O(n logn) SC= O(1)        //This is only optimised  for returning Yes/ No if two sum exists
    string twoSumExists(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0, right = n - 1;
        sort(nums.begin(), nums.end());

        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) return "YES";
            else if (sum < target) left++;
            else right--;
        }
        return "NO";
    }
Sort Array of 0's 1's and 2's
## Brute Force TC= O(n logn) SC= O(n)        //Simply sorted using any sort (eg: Merge sort)
    void Mergesort(vector<int>& nums, int left, int right){
        if(left >= right) return;
        int mid = (left+right)/2;
        Mergesort(nums, left, mid);
        Mergesort(nums, mid+1, right);
        Merge(nums, left, mid, right);
    }
    void Merge(vector<int>& nums, int left, int mid, int right) {
        vector<int> temp;
        int i = left;       
        int j = mid + 1;  
        while (i <= mid && j <= right) {
            if (nums[i] <= nums[j]) {
                temp.push_back(nums[i]);
                i++;
            } else {
                temp.push_back(nums[j]);
                j++;
            }
        }
        while (i <= mid) {
            temp.push_back(nums[i]);
            i++;
        }
        while (j <= right) {
            temp.push_back(nums[j]);
            j++;
        }
        for (int k = 0; k < temp.size(); k++) {
            nums[left + k] = temp[k];
        }
    }
    void sortZeroOneTwo(vector<int>& nums){
        Mergesort(nums, 0, nums.size()-1);
    }
## Average Approach TC= O(2n) 
    void sortZeroOneTwo(vector<int>& nums) {
        int cnt0 = 0, cnt1 = 1, cnt2 = 2;
        int n= nums.size();
        for(int i=0; i<n; i++){
            if(nums[i] == 0) cnt0++;
            else if(nums[i] == 1) cnt1++;
            else cnt2++;
        }
        for(int i=0; i<cnt0; i++) nums[i]= 0;
        for(int i=cnt0; i<cnt0+cnt1; i++) nums[i]= 1;
        for(int i=cnt0+cnt1; i<n; i++) nums[i]= 2;
    }
## Optimal Approach TC= O(n)        //Dutch National FLag Algorithn
    void sortZeroOneTwo(vector<int>& nums) {
        int n= nums.size();
        int low=0, mid=0, high= n-1;
        while(mid<=high){
            if(nums[mid] == 0){
                swap(nums[low], nums[mid]);
                low++; mid++;
            }
            else if(nums[mid] == 1){
                mid++;
            }
            else{       //(nums[mid] == 2)
                swap(nums[mid], nums[high]);
                high--;
            }
        }
    }
Majority Elements
## Brute Force TC= O(n^2)
    int majorityElement(vector<int>& nums) {
        int n= nums.size();
        for(int i=0; i<n; i++){
            int cnt=0;
            for(int j=0; j<n; j++){
                if(nums[j] == nums[i]) cnt++;   
            }
            if(cnt>n/2) return nums[i];
        }
        return -1;
    }
## Better Approach TC= O(n logn) SC= O(n)
    int majorityElement(vector<int>& nums) {
        int n= nums.size();
        map<int, int>mpp;                    //for map TC= nlogn for Unordered map TC = n
        for(int i=0; i<n; i++){
            mpp[nums[i]]++;
        }
        for(auto it: mpp){
            if(it.second > n/2) return it.first;
        }
        return -1;
    }
## Optimised Approach TC= O(n)        //Moore Voting Algorithm
    int majorityElement(vector<int>& nums) {
        int n= nums.size();
        int cnt=0;
        int ele;
        for(int i=0; i<n; i++){
            if(cnt == 0){
                cnt=1;
                ele= nums[i];
            }
            else if(nums[i] == ele) cnt++;
            else cnt--; 
        }
        return ele;
    }
Maximum SubArray Sum
## Brute Force TC= O(n^3)
    int maxSubArray(vector<int>& nums) {
        int n= nums.size();
        int maxi= INT_MIN;
        for(int i=0; i<n; i++){
            for(int j=i; j<n; j++){
                int sum= 0;
                for(int k=i; k<=j; k++){
                    sum+= nums[k];
                }  
                maxi= max(maxi, sum);
            }
        }
        return maxi;
    }
## Average Approach TC= O(n^2)
    int maxSubArray(vector<int>& nums) {
        int n= nums.size();
        int maxi= INT_MIN;
        for(int i=0; i<n; i++){
            int sum= 0;
            for(int j=i; j<n; j++){
                sum+= nums[j];
            }
            maxi= max(maxi, sum);
        }
        return maxi;
    }
## Optimal Approach TC= O(n)        //Kadane Algorithm
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        int maxSum = INT_MIN;
        int start = 0, ansStart = -1, ansEnd = -1;
        for (int i = 0; i < n; i++) {
            if (sum == 0) start = i;   
            sum += nums[i];
            if (sum > maxSum) {
                maxSum = sum;
                ansStart = start;
                ansEnd = i;
            }
            if (sum < 0) {
                sum = 0;   // reset if sum becomes negative
            }
        }
        return maxSum;
    }

    //For printing the subarray
    for (int i = ansStart; i <= ansEnd; i++) {
        cout << nums[i];
    }
Stock Buy and Sell # Part I
## Brute Force TC= O(n)
    int stockBuySell(vector<int> arr, int n){
        int mini= arr[0];
        int profit=0;
        for(int i=0; i<n; i++){
            int cost= arr[i]- mini;
            profit= max(profit, cost);
            mini= min(mini, arr[i]);
        }
        return profit;
    }
Rearrange the Array in Alternate Positive and Negative items
## Brute Force TC= O(n) SC= O(n)
    vector<int> rearrangeArray(vector<int>& nums) {
        int n= nums.size();
        vector<int> ans(n, 0);
        int pos=0, neg=1;
        for(int i=0; i<n; i++){
            if(nums[i] < 0){
                ans[neg] = nums[i];
                neg += 2;
            }
            else{
                ans[pos] = nums[i];
                pos += 2;
            }
        }
        return ans;
    }
## Optimal Solution TC=O(2n)
    vector<int> rearrangeArray(vector<int>& nums) {
        vector<int> pos, neg;
        int n= nums.size();
        //general case
        for(int i=0; i<n; i++){
            if(nums[i]<0){
                neg.push_back(nums[i]);
            }
            else pos.push_back(nums[i]);
        }
        //this section is if either way pos>neg or neg>pos
        if(pos.size()>neg.size()){
            for(int i=0; i<neg.size(); i++){
                nums[2*i]= pos[i];
                nums[2*i+1] = neg[i];
            }//now the remaining pos elements
            int index= (neg.size()*2);
            for(int i= neg.size(); i<pos.size(); i++){
                nums[index] = pos[i];
                index++;
            }
        }
        else{
            for(int i=0; i<pos.size(); i++){
                nums[2*i]= pos[i];
                nums[2*i+1]= neg[i];
            }//now the remaining neg elements
            int index= (pos.size()*2);
            for(int i= pos.size(); i<neg.size(); i++){
                nums[index] = neg[i];
                index++;
            }
        }
        return nums;
    }
Next Permutation
## TC= O(n)        //Longest Prefix Match and Dip finding
    vector<int> nextPermutation(vector<int>& nums) {
        int n= nums.size();
        int ind= -1;
        for(int i= n-2; i>= 0; i--){
            if(nums[i]<nums[i+1]){
                ind = i;
                break;
            }
        }
        if(ind == -1){
            reverse(nums.begin(), nums.end());
            return nums;
        } 
        for(int i= n-1; i> ind; i--){
            if(nums[i] > nums[ind]){
                swap(nums[i], nums[ind]);
                break;
            }
        }
        reverse(nums.begin()+ ind+1, nums.end());
        return nums;
    }
Leaders in Array
## Brute Force TC= O(n^2) 
    vector<int> leaders(vector<int>& nums) {
        int n= nums.size();
        vector<int> ans;
        for(int i=0; i<n; i++){
            bool leader= true;
            for(int j= i+1; j<n; j++){
                if(nums[j]>nums[i]){
                    leader = false;
                    break;
                }
            }
            if(leader == true) ans.push_back(nums[i]);
        }
        return ans;
    }
## Optimal Solution TC= O(n)
    vector<int> leaders(vector<int>& nums) {
        //O(N)
        int n= nums.size();
        vector<int> ans;
        int maxi= INT_MIN;
        //O(N)
        for(int i=n-1; i>=0; i--){
            if(nums[i]>=maxi){
                ans.push_back(nums[i]);
            }
            maxi= max(maxi, nums[i]);
        }
        //O(N logN)
        reverse(ans.begin(), ans.end());
        return ans;
    }
Longest Consecutive Sequence in an Array
## Brute Force TC= O(n^2)
    bool ls(vector<int>& nums, int val, int n){
        for(int i=0; i<n; i++){
            if(nums[i] == val) return true;
        }
        return false;
    }
    int longestConsecutive(vector<int>& nums) {
        int n= nums.size();
        if(n == 0) return 0;
        int longest= 1;
        int x,cnt=0;
        for(int i=0; i<n; i++){
            x= nums[i];
            cnt=1;
            while(ls(nums, x+1, n) == true){
            x++;    //ls(nums, x+1) linear search is done for x+1 element in nums
            cnt++;
            }
            longest= max(longest, cnt);
        } 
        return longest;
    }
## Average Approach TC= O(n logn)
    int longestConsecutive(vector<int>& nums) {
        int n= nums.size();
        if(n == 0) return 0;
        sort(nums.begin(), nums.end());
        int lastsmaller= INT_MIN;
        int cnt=0;
        int longest =1;
        for(int i=0; i<n; i++){
            if(nums[i] -1 == lastsmaller){
                cnt++;
                lastsmaller= nums[i];
            }
            else if(lastsmaller != nums[i]){
                cnt =1;
                lastsmaller = nums[i];
            }
            longest= max(longest, cnt);
        }
        return longest;
    }
## Optimal Approach TC= O(n) SC= O(n)
    int longestConsecutive(vector<int>& nums) {
        int n= nums.size();
        if(n == 0) return 0;
        int longest= 1;
        unordered_set<int> st;
        for(int i=0; i<n; i++){
            st.insert(nums[i]);
        }
        for(auto it: st){
            if(st.find(it-1) == st.end()){  //to check if it dont have a smaller number than it in the sequence
                int cnt =1;
                int x = it;         //if it dont have a smaller number then its the start of the sequence as x
                while(st.find(x+1) != st.end()){
                    x = x+1;
                    cnt++;
                }
                longest= max(longest, cnt);
            }
        }
        return longest;
    }
Set Matrix Zeroes
## Brute Force TC= O(n^3) 
    void markRow(vector<vector<int>>& arr, int i, int m) {
        for(int j=0; j<m; j++){
            if(arr[i][j] != 0) arr[i][j] = -1;
        }
    }

    void markCol(vector<vector<int>>& arr, int j, int n) {
        for(int i=0; i<n; i++){
            if(arr[i][j] != 0) arr[i][j] = -1;
        }
    }

    void setZeroes(vector<vector<int>>& arr) {
        int n = arr.size();
        int m = arr[0].size();

        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(arr[i][j] == 0){
                    markRow(arr, i, m);
                    markCol(arr, j, n);
                }
            }
        }

        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(arr[i][j] == -1) arr[i][j] = 0;
            }
        }
    }
## Average Approach TC= O(n^2) SC= O(n)
    void setZeroes(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        vector<int> row(n, 0), col(m, 0);

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(matrix[i][j] == 0){
                    row[i] = 1;
                    col[j] = 1;
                }
            }
        }

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(row[i] || col[j]){
                    matrix[i][j] = 0;
                }
            }
        }
    }
## Optimal Solution TC= O(n^2)
    void setZeroes(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        int col0 = 1;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(matrix[i][j] == 0){
                    matrix[i][0] = 0; // mark row
                    if(j != 0) matrix[0][j] = 0; // mark col
                    else col0 = 0;
                }
            }
        }

        for(int i = 1; i < n; i++){
            for(int j = 1; j < m; j++){
                if(matrix[i][0] == 0 || matrix[0][j] == 0){
                    matrix[i][j] = 0; 
                }
            }
        }

        if(matrix[0][0] == 0){
            for(int j = 0; j < m; j++) matrix[0][j] = 0;
        }

        if(col0 == 0){
            for(int i = 0; i < n; i++) matrix[i][0] = 0;
        }
    }
Rotate Matrix by 90 Degrees
## Brute Force TC= O(n^2) SC= O(n^2)
    void rotateMatrix(vector<vector<int>>& matrix) {
        int n = matrix.size();
        vector<vector<int>> ans(n, vector<int>(n));
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                ans[j][n - 1 - i] = matrix[i][j];
            }
        }
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                matrix[i][j] = ans[i][j];
            }
        }
    }
## Optimised Approach TC= O(n^2)
    void rotateMatrix(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for(int i=0; i<n-1; i++){
            for(int j= i+1; j<n; j++){
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for(int i=0; i<n; i++){
            //reverse the rows i.e matrix[i]
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
Print the Matrix in Spiral Manner
## Brute Force TC= O


Count SubArrays with Given Sum
## Brute Force TC= O(n^3)
    int subarraySum(vector<int> &nums, int k) {
        int n = nums.size();
        int cnt = 0;
        for(int i = 0; i < n; i++){
            for(int j = i; j < n; j++){
                int sum = 0;
                for(int x = i; x <= j; x++){ 
                    sum += nums[x];
                }
                if(sum == k) cnt++;
            }
        }
        return cnt;
    }
## Better Approach TC= O(n^2)
    int subarraySum(vector<int> &nums, int k) {
        int n = nums.size();
        int cnt = 0;
        for(int i = 0; i < n; i++){
            int sum = 0;
            for(int j = i; j < n; j++){
                sum += nums[j];
                if(sum == k) cnt++;
            }
        }
        return cnt;
    }
## Optimal Approach TC= O(n logn) SC= O(n)       //PREFIX SUM with hash map     //for unordered map its TC = O(n)
    int subarraySum(vector<int> &nums, int k) {
        int n = nums.size();
        map<int, int> mpp;
        mpp[0] = 1;
        int prefixsum=0, cnt = 0;
        for(int i=0; i<n; i++){
            prefixsum+=nums[i];
            int remove = prefixsum-k;
            cnt+=mpp[remove];
            mpp[prefixsum]+=1;
        }
        return cnt;
    }
Print the Matrix in Spiral Form
## Only Approach TC= O(n * m)
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n= matrix.size();
        int m= matrix[0].size();
        int left=0, right= m-1;
        int top=0, bottom= n-1;
        vector<int> ans;

        while(top<=bottom && left<=right){
            //right
            for(int i=left; i<=right; i++){
                ans.push_back(matrix[top][i]);
            } top++;
            //bottom
            for(int i=top; i<=bottom; i++){
                ans.push_back(matrix[i][right]);
            } right--;
            //left
            if(top<=bottom){
                for(int i=right; i>= left; i--){
                    ans.push_back(matrix[bottom][i]);
                } bottom--;
            }
            //top
            if(left<=right){
                for(int i=bottom; i>=top; i--){
                    ans.push_back(matrix[i][left]);
                } left++;
            }
        }
        return ans;
    }
