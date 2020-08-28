# my_compositions
my compositions for orchestral instrumentation using Sibelius and other tools

/* Longest Palindrome in a string O(n3) brute */

/* Exhaustive search. i at 0, j scans all
 * from i to n. record max. then i = 1 etc till
 * i = n. Then find optimizations 
 */

char * printReverseString(char * s){
    
    int len = strlen(s);
    char* end = s + len;
    
    /* reverse print check */
    int i = len;
    while(i >= 0) {
        printf("%c", *end);
        end--; i--;
    }
    
    printf("\n");
    return NULL;
}

bool isPalindrome(char * s, int len) {
    
    int i = 0, j = len-1;
            
    /* if len is odd ignore the middle number */
    
    while (i < j) {
        if(s[i] != s[j]) return false;
        i++; j--;
    }

    return true;    
}

char * longestPalindrome(char * s) {
    
    int len = strlen(s);
    if (len == 0 || len == 1) return s;
    
    char* retString = (char*)malloc(sizeof(char) * 1001); // heap to return
    int i = 0; int j = 0;
    
    /* lazy: get the actual indexes first, fill up later */
    int start_retIndex = 0;
    int max_retLen = 1;  /* OP assumes every single letter is a pal and wants leftmost so complying */
    
    while (i <= len-1) {
        
        j = i + 1; 
        while( j <= len-1) {
            
            //printf("\ncheck %d %d\n", i, j);
            int thislen = j - i + 1; // can check if thislen > 1000 for sanity
            if (isPalindrome( (char*) (s+i), thislen)) {
                
                /* if this is a current max grab it */
                if (max_retLen < thislen) {
                    max_retLen = thislen;
                    start_retIndex = i;
                }
            }
            j++;
        }   
        i++;
    }
    
    /* generate the max palindrome if any */    
    for(i = 0; i < max_retLen; i++) {
        retString[i] = s[start_retIndex + i];
    }
    retString[i] = '\0';
            
    /* for duplicate max pals this will return the leftmost max pal */
    return retString;
}
