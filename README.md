document.getElementById('submitBtn_3').addEventListener('click', function() {
  // Get all time-slot-1 elements
  const firstSlots = document.querySelectorAll('.time-slot-1');
  
  firstSlots.forEach((slot, index) => {
    // Get status from time-slot-1
    const statusDiv1 = slot.nextElementSibling;
    if (!statusDiv1 || !statusDiv1.classList.contains('status-div-1')) return;
    
    const status = statusDiv1.textContent;
    
    // Find corresponding time-slot-2 (same row)
    const row = slot.closest('.content-row');
    const timeSlot2 = row.querySelector('.time-slot-2');
    if (!timeSlot2) return;
    
    // Remove existing status-div-2 if present
    const existingStatus2 = timeSlot2.nextElementSibling;
    if (existingStatus2 && existingStatus2.classList.contains('status-div-2')) {
      existingStatus2.remove();
    }
    
    // Create new status-div-2
    const statusDiv2 = document.createElement('div');
    statusDiv2.className = 'status-div-2';
    statusDiv2.textContent = status;
    statusDiv2.dataset.status = status.toLowerCase();
    timeSlot2.insertAdjacentElement('afterend', statusDiv2);
  });
  
  // Visual feedback
  const copyBtn = document.getElementById('copyBtn');
  copyBtn.textContent = 'Copied!';
  setTimeout(() => {
    copyBtn.textContent = 'Copy Status to Slot 2';
  }, 2000);
});


//  leetcode (Two Letter Card Game) 

class Solution {
public:
    int score(vector<string>& cards, char x) {

        int ans = 0;
        int f = 0;
        int tf = 0;
        int s = 0;
        int ts = 0;
        int xx = 0;
        int used = 0;
        vector<int> dict1(26, 0);
        vector<int> dict2(26, 0);
        
        for (int i = 0; i < cards.size(); ++i) {

            char c1 = cards[i][0];
            char c2 = cards[i][1];

            if (c1 == x && c2 == x)
                xx++;
            else if (c1 == x) {

                dict1[c2 - 'a']++;
                f = max(dict1[c2 - 'a'], f);
                tf++;
                
            } else if (c2 == x) {

                dict2[c1 - 'a']++;
                s = max(dict2[c1 - 'a'], s);
                ts++;
            }
        
        }

        if (f > (tf - f)) {

            ans += (tf - f);
            tf = f - (tf - f);
            
        } else {

            ans += tf / 2;
            tf = tf % 2;
        }

        
        if (s > (ts - s)) {

            ans += (ts - s);
            ts = s - (ts - s);
            
        } else {

            ans += ts / 2;
            ts = ts % 2;
        }

        used += min(tf + ts, xx);
        xx -= min(tf + ts, xx);         
        ans = min(ans * 2, ans + xx / 2);
        ans += used;
        
        return ans;
    }
};




