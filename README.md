# problem_solution
knight tour problem


#include<iostream>
#include<iomanip>
using namespace std;

const int d=6;

bool canPlace(int board[d][d],int n,int r,int c){
    return
        r>=0&&r<n&&
        c>=0&&c<n&&
        board[r][c]==0;
}

bool solveknight(int board[d][d],int n,int move_no,int curRow,int curCol){

    if(move_no==n*n)
    {
        return true;
    }
    int rowDir[]={2,1,-1,-2,-2,-1,1,2};
    int colDir[]={1,2,2,1,-1,-2,-2,-1};
    for(int curDir=0;curDir<8;curDir++){
        int nextRow=curRow+rowDir[curDir];
        int nextCol=curCol+colDir[curDir];
        if(canPlace(board,n,nextRow,nextCol)==true){
            board[nextRow][nextCol]=move_no+1;
            bool isSuccessfull=solveknight(board,n,move_no+1,nextRow,nextCol);
            if(isSuccessfull==true){
                return true;
            }
            board[nextRow][nextCol]=0;
        }
    }

  return false;
}
void printboard(int board[d][d],int n)
{
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<n;j++){
            cout<<setw(3)<<board[i][j]<<"  ";
        }
        cout<<endl;
    }
}

int main(){

    int board[d][d]={0};
    int n;
    cin>>n;
    board[0][0]=1;
    bool ans=solveknight(board,n,1,0,0);
    if(ans==true)
    {
        printboard(board,n);
    }
    else
        cout<<"no such move";
}
