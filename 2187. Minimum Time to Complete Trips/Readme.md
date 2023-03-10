# Problem: Minimum Time to Complete Trips

Platform: Leetcode

Difficulty: Medium

Problem Link: https://leetcode.com/problems/minimum-time-to-complete-trips/

## Problem Statement:

You are given an array time where time[i] denotes the time taken by the ith bus to complete one trip.

Each bus can make multiple trips successively; that is, the next trip can start immediately after completing the current trip. Also, each bus operates independently; that is, the trips of one bus do not influence the trips of any other bus.

You are also given an integer totalTrips, which denotes the number of trips all buses should make in total. Return the minimum time required for all buses to complete at least totalTrips trips.

 

Example 1:

    Input: time = [1,2,3], totalTrips = 5
    Output: 3
    Explanation:
    - At time t = 1, the number of trips completed by each bus are [1,0,0]. 
    The total number of trips completed is 1 + 0 + 0 = 1.
    - At time t = 2, the number of trips completed by each bus are [2,1,0]. 
    The total number of trips completed is 2 + 1 + 0 = 3.
    - At time t = 3, the number of trips completed by each bus are [3,1,1]. 
    The total number of trips completed is 3 + 1 + 1 = 5.
    So the minimum time needed for all buses to complete at least 5 trips is 3.

## Solution (In Java):

    class Solution {
        public long minimumTime(int[] time, int totalTrips) {
            long l = 1;
            long r = Arrays.stream(time).min().getAsInt() * (long) totalTrips;

            while (l < r) {
            final long m = (l + r) / 2;
            if (numTrips(time, m) >= totalTrips)
                r = m;
            else
                l = m + 1;
            }

            return l;
        }

        private long numTrips(int[] time, long m) {
            return Arrays.stream(time).asLongStream().reduce(0L, (subtotal, t) -> subtotal + m / t);
        }
    }


## Output:
<img
  src="Output.png"
  alt="Alt text"
  title="Optional title"
  style="display: inline-block; margin: 0 auto; max-width: 300px">








