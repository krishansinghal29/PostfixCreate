/*
// Sample code to perform I/O:

#include <iostream>

using namespace std;

int main() {
	int num;
	cin >> num;										// Reading input from STDIN
	cout << "Input number is " << num << endl;		// Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/

// Write your code here
/*
// Sample code to perform I/O:

#include <iostream>

using namespace std;

int main() {
	int num;
	cin >> num;										// Reading input from STDIN
	cout << "Input number is " << num << endl;		// Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/

// Write your code here
#include <iostream>
using namespace std;
class stackk 
{
   public:
      int top=-1;   // Length of a box
      //vector<char> st;  // Breadth of a box
      //vector<int> pr;
      char st[1000000];
      int pr[1000000];
      int empty(){
         if(top==-1){
             return 1;
         }
         else{
             return 0;
         }
      }
      char pop(){
          if(top==-1){
             printf("Error");
          }
          else{
              top=top-1;
              char out=st[top+1];
              //pr.resize(top+1);
              //aso.resize(top+1);
              //st.resize(top+1);
              return out;
          }
      }
      void push(char i,int j){
          top=top+1;
          pr[top]=j;
          //aso.push_back(k);
          st[top]=i;
          return ;
      }
};
int precedence(char l,int i){
    int asci=(int)(l);
    //int a=(int)('^'); int b=(int)('/');  int c=(int)('%');  int d=(int)('*');  int e=(int)('+');  int f=(int)('-');
    int ans;
    switch (asci) 
   { 
       case (int)('~'): ans=4+10*i;
               break; 
       case (int)('^'): ans=3+10*i;
               break; 
       case (int)('/'): ans=2+10*i; 
                break; 
       case (int)('%'): ans=2+10*i; 
               break; 
       case (int)('*'): ans=1+10*i;
               break; 
       case (int)('+'): ans=0+10*i; 
                break; 
       case (int)('-'): ans=0+10*i; 
               break; 
       default: ans=-1; 
               break;   
   } 
   return ans;
}

int main(){
    int cases;
    scanf("%d\n",&cases);
    for(int j=0;j<cases;j++){
        //string input;
        //getline(cin,input);
        //string output;
        int indx=0;
        int u=0;
        char *output = (char *) malloc(1000000* sizeof (char));
        int outlen=0;
        char *input = (char *) malloc(1000000* sizeof (char));
        scanf("%[^\n]\n",input);
        int lens=0;
        while(input[lens]!='\0'){
            lens++;
        }
        //int bracket=0;
        int previous=0;
        char inpt=input[indx];
        int i=0;
        //int k=0;
        //printf("%d",(input[9]=='NULL'));
        stackk S; 
        while(indx<lens){
            
            int inte=(int)(inpt-'0');
            if(inte<10&&inte>-1){
                u=0;
                //bracket==0;
                if(previous==-1){
                    previous=1;
                    printf("INVALID\n");
                    break;
                }
                previous=-1;
                int i=1;
                outlen++;
                output[outlen-1]=inpt;
                while(((int)(input[indx+1]-'0'))<10&&((int)(input[indx+1]-'0'))>-1&&(indx+1<lens)){
                    inte=10*inte+(int)(input[indx+1]-'0');
                    indx++;
                    i++;
                    outlen++;
                    output[outlen-1]=input[indx];
                }
                //string out=to_string(inte);
                //output.append(out);
                //output.push_back(' ');
                outlen++;
                output[outlen-1]=' ';
                //printf("%d ",inte);
                
            }
            else if(inpt=='('){
                i=i+1;
                u=1;
                // if(bracket==1){
                //     previous=1;
                //     printf("INVALID\n");
                //     break;
                // }
                //bracket=1;
            }
            else if(inpt==')'){
                i=i-1;
                // if(bracket==1){
                //     previous=1;
                //     printf("INVALID\n");
                //     break;
                // }
                // bracket=0;
                u=0;
                if(i==-1){
                    previous=1;
                    printf("INVALID\n");
                    break;
                }
            }
            else{
                //bracket==0;
                int as=0;
                
                if(previous==-1&&u==1&&inpt=='-'){
                    inpt='~';
                    as=1;
                }
                u=0;
                if(inpt=='^'){
                    as=1;
                }
                if(precedence(inpt,i)==-1||precedence(inpt,0)==4){
                    previous=1;
                    printf("INVALID\n");
                    break;
                }
                
                if(previous!=-1&&inpt=='-'){
                    inpt='~';
                    as=1;
                }
                else if(previous!=-1){
                    previous=1;
                    printf("INVALID\n");
                    break;
                }
                // else if(previous==2){
                //     previous=1;
                //     printf("INVALID\n");
                //     break;
                // }
                // int pre=0;
                // if(inpt=='~'){
                //     pre=2;
                // }
                // previous=pre;
                previous=0;
                
                while((S.empty()!=1)&&((precedence(inpt,i)+as)<=S.pr[S.top])){
                    outlen++;
                    output[outlen-1]=S.pop();
                    outlen++;
                    output[outlen-1]=' ';
                    //printf("%c ",S.pop());
                    //printf("%c ",inpt);
                }
                S.push(inpt,precedence(inpt,i));
                
                //printf("%c ",inpt);
            }
            if((indx+1)<lens){
                if(input[indx+1]!=' '){
                    previous=1;
                    printf("INVALID\n");
                    break;
                }
            }
            indx=indx+2;
            inpt=input[indx];
        }
        if(previous==1){
            continue;
        }
        if(i>0&&previous!=1){
            printf("INVALID\n");
            continue;
        }
        if(precedence(input[indx-2],0)!=-1){
            printf("INVALID\n");
            continue;
        }
        
        //printf("%c ",S.st[0]);
        while(S.empty()!=1){
            outlen++;
            output[outlen-1]=S.pop();
            outlen++;
            output[outlen-1]=' ';
            //printf("%c ",S.pop());
            //printf("%d ",S.top);
        }
        // if(output.length()==0){
        //     printf("INVALID\n");
        //     continue;
        // }
        //int a=65;
        //string a=string(a)
        //printf("%d\n",output.length());
        for(int k=0;k<outlen-1;k++){
            printf("%c",output[k]);
        }
        printf("\n");
        //printf("%s\n",output.c_str());
        free(input);
        free(output);
        //printf("\n");
    }
    return 0;
}
