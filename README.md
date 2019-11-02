// Longest Increasing Subsequence
// Time Complexity O(nlogn) 
// Space Complexity O(n)
// 'n' is length of the given array


// this is binary search, to search the least element in temp just greater than equal to target
int get(vector<int> temp,int start,int end,int target){
    if(start>end) return INT_MAX;
    if(start==end){
        return (temp[start]>=target)?start:INT_MAX;
    }
    int mid=(start+end)/2;
    if(temp[mid]>=target)
        return min(mid,get(temp,start,mid-1,target));
    else return get(temp,mid+1,end,target);
}

int Solution::lis(const vector<int> &A) {
    int len=1;
    vector<int> max_at(A.size()+1);
    max_at[1]=A[0];
    for(int i=1;i<A.size();i++){
        if(A[i]<max_at[1])
            max_at[1]=A[i];
        else if(A[i]>max_at[len]){
            max_at[len+1]=A[i];
            len++;
        }
        else{
            int t=get(max_at,1,len,A[i]);
            max_at[t]=A[i];
        }
    }
    return len;
}
