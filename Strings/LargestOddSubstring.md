📒 Notes – Largest Odd Number in String
🔹 Problem Statement

Tumhe ek numeric string num di gayi hai (sirf digits hoti hain).

Tumhe sabse bada odd number return karna hai jo num ke prefix (starting se koi substring) se ban sakta hai.

Agar koi odd digit hi na ho → return "".

🔹 Key Observations

Odd number ke liye last digit odd honi chahiye (1, 3, 5, 7, 9).

Isliye hume right to left traverse karna hoga.

Jahan pehle odd digit mile → wahi takka prefix hi answer hoga.

Kyunki uske aage jitna bhi number hai, wo usi prefix se hi odd number banayega.

🔹 Important Trick

Digit char ko integer me convert karne ke liye:

int digit = ch - '0';


'0' = 48 (ASCII)

'7' = 55

'7' - '0' = 7

Fastest method hai character → digit conversion ke liye.

🔹 Approach

Traverse string end se start.

Har char ko digit me convert karo (ch - '0').

Agar odd digit mila → return num.substring(0, i+1).

Agar pura traverse kar liya aur odd nahi mila → return "".

🔹 Code
class Solution {
    public String largestOddNumber(String num) {
        for (int i = num.length() - 1; i >= 0; i--) {
            int digit = num.charAt(i) - '0';
            if (digit % 2 == 1) {
                return num.substring(0, i + 1);
            }
        }
        return "";
    }
}

🔹 Dry Run Example

s = "35420"

i=4 → '0' (even)

i=3 → '2' (even)

i=2 → '4' (even)

i=1 → '5' (odd ✅)
→ return num.substring(0, 2) = "35"

Output = "35"

🔹 Time & Space Complexity

Time: O(n) → ek hi baar traverse karte hain.

Space: O(1) → extra space nahi lagta (substring view hi hai).

class Solution {
    public String largestOddNumber(String num) {
        int maxnumber = 0;
        for(int i = num.length()-1;i>=0;i--){
            char ch = num.charAt(i);
            int digit = ch-'0';
            if(digit%2!=0){
                return num.substring(0,i+1);
            }
        }
        
        return "";
    }
}
